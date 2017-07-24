# Problem:

The output of the code below are not always __true__, why?

```java
import java.util.HashMap;
import java.util.Map;

public class EqualsTest {

    public static void main(String[] args) {
        forLoop();
        testMap();
    }

    public static void forLoop() {
        for (int i = 0; i < 150; i++) {
            Integer a = i;
            Integer b = i;
            System.out.println(i + " " + (a == b));
        }
    }

    public static void testMap() {
        Map<Integer, Integer> mapA = new HashMap<>();
        Map<Integer, Integer> mapB = new HashMap<>();
        for (int i = 0; i < 150; i++) {
            mapA.put(i, i);
            mapB.put(i, i);
        }
        for (int i = 0; i < 150; i++) {
            System.out.println(i + " " + (mapA.get(i) == mapB.get(i)));
        }
    }
}
```

# Answer
//The reason is Java's autoboxing. The numbers started as __int__ in [0, 127], but in [128, 149] they are compared as __Integer__. The " == " in non-premitive classes are comparing the reference to see whether they are the same object or not.

# Source Code
```java
/**
    * Returns an {@code Integer} instance representing the specified
    * {@code int} value.  If a new {@code Integer} instance is not
    * required, this method should generally be used in preference to
    * the constructor {@link #Integer(int)}, as this method is likely
    * to yield significantly better space and time performance by
    * caching frequently requested values.
    *
    * This method will always cache values in the range -128 to 127,
    * inclusive, and may cache other values outside of this range.
    *
    * @param  i an {@code int} value.
    * @return an {@code Integer} instance representing {@code i}.
    * @since  1.5
    */
public static Integer valueOf(int i) {
    if (i >= IntegerCache.low && i <= IntegerCache.high)
        return IntegerCache.cache[i + (-IntegerCache.low)];
    return new Integer(i);
}

```

```java
private static class IntegerCache {
    static final int low = -128;
    static final int high;
    static final Integer cache[];

    static {
        // high value may be configured by property
        int h = 127;
        String integerCacheHighPropValue =
            sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
        if (integerCacheHighPropValue != null) {
            try {
                int i = parseInt(integerCacheHighPropValue);
                i = Math.max(i, 127);
                // Maximum array size is Integer.MAX_VALUE
                h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
            } catch( NumberFormatException nfe) {
                // If the property cannot be parsed into an int, ignore it.
            }
        }
        high = h;

        cache = new Integer[(high - low) + 1];
        int j = low;
        for(int k = 0; k < cache.length; k++)
            cache[k] = new Integer(j++);

        // range [-128, 127] must be interned (JLS7 5.1.7)
        assert IntegerCache.high >= 127;
    }

    private IntegerCache() {}
}
```
When IntegerCache is loading, the static block will be executed first, [-128, 127] will be initialized as __int__for later use.

# Solution
```java
for (int i = 0; i < 150; i++) {
    Integer a = i;
    Integer b = i;
    System.out.println(i + " " + (a.equals(b)));
}
```

#### Reference:

  * https://www.polarxiong.com/archives/Java-Integer%E7%94%A8-%E6%AF%94%E8%BE%83%E6%97%B6127%E7%9B%B8%E7%AD%89128%E4%B8%8D%E7%9B%B8%E7%AD%89%E7%9A%84%E5%8E%9F%E5%9B%A0.html
  * http://rednaxelafx.iteye.com/blog/680746

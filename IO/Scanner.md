# Scanner

The __Scanner__ constructor can take just any kind of input object, including a __File__ object, an __InputStream__, a __String__ or this 
case a __Readable__, which is an interface introduced in Java SE5 to describe "something that has a __read()__ method."

With __Scanner__, the input, tokenizing, and parsing are all ensconced in various different kinds of "next" methods. A plain __next()__
returns the next __String__ token, and there are "next" methods for all the primitive types(except __char__) as well as for __BigDecimal__
and __BigInteger__. All of the "next" methods _block_, meaning they will return only after a complete data token is available for input.
 There are also corresponding "hasNext" methods that return __true__ if the next input token is the correct type. 
 
The __Scanner__ makes assumptions that an __IOException__ signals the end of input, and so these are swallowed by the __Scanner__.


#### Reference
 * http://blog.sina.com.cn/s/blog_81547cad01018mnd.html
 * https://www.hackerrank.com/challenges/java-stdin-stdout/forum


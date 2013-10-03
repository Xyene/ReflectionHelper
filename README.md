ReflectionHelper
================

Fluent generic Java reflection.

Compilation
-----------

We use [Maven](http://maven.apache.org/download.html) to handle our dependencies.

Usage
-----

ReflectionHelper is designed to be easy to use with a fluent interface.

The following code demonstrates the capabilities of ReflectionHelper.

```java
package tk.ivybits.reflection;

public class Main {
    private static final String message = "Reflection is fun again!";

    public static void main(String[] args) throws Exception {
        String value = Reflection.declaredField("message")
                .in(Main.class)
                .ofType(String.class)
                .get();

        assert message !=  value;

        String str = Reflection.constructor()
                .in(String.class)
                .withParameters(String.class)
                .newInstance(value);

        assert !(message.equals(str));

        assert str.length() != Reflection.declaredMethod("length")
                .in(str)
                .withReturnType(int.class)
                .invoke();
    }
}
```

ReflectionHelper also performs a few things to ease your job as a developer.

* Wraps all thrown `Exception`s with a `RuntimeException`: you need not catch anything
* Handles member visibility access
* Can set final fields under some circumstances

If you wish to do your own dirty work, you may at any time use the `getRaw` method in any member container.
It will return the `java.lang.reflect` equivalent, providing enough information was specified for ReflectionHelper
to find it.
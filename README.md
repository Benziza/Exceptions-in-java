# Exceptions-in-java

## 1-The concept of exceptions in Java

**Exception** (Exceptions) in programming is an error that occurs during the operation of the program leads to stop it abnormally.

## 2-Exception categories

Exceptions may occur because of the user (User), or the programmer (Programmer), or because of the devices used (Physical Resources).

Based on this, the exceptions are divided into three main categories:

- **Checked Exception**: A code error that occurs while compiling the program (i.e. before running the code).
- **Unchecked Exception**: means a logical error that occurs while the program is running.
- **Error**: means an error caused by the device we are trying to run the program on.

### 2-1-Checked Exception

Example :

```
public class Main {

    public static void main(String[] args) {

        int a;
        a = "this is incompatible type, 'a' should be String";

    }

}
```

The following error will appear if we run the program.

```
Exception in thread "main" java.lang.RuntimeException: Uncompilable source code - incompatible types: java.lang.String cannot be converted to int
```

### 2-2-Unchecked Exception

Unchecked Exception means an exception that occurs during the operation of the program, and it is also called Runtime Exception, and it includes Programming Bugs, which mean logical errors or errors caused by not using the objects defined in the programming language correctly (APIs errors).

```
public class Main {

    public static void main(String[] args) {

        int[] a = { 1, 2, 3, 4, 5 };
        System.out.println( a[10] );

    }

}
```

The following error will appear if we run the program.

```
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 10
```

### 2-3-Error

Error means an error caused by the device on which we are trying to run the program, the program has nothing to do with this error.

For example, if the memory of the device on which the program is running is full, an error will occur, which is that the operating system cannot run this program because the device's memory is full. And then the following message will appear to explain the error _JVM is out of Memory_

## 3-Exception constructing in java

Exceptions are built in an orderly manner as in the following picture.
![alt text](https://media.geeksforgeeks.org/wp-content/uploads/Exception-in-java1.png)

### 3-1-Unchecked Exception

|            Exception            |
| :-----------------------------: |
|       ArithmeticException       |
| ArrayIndexOutOfBoundsException  |
| StringIndexOutOfBoundsException |
|       ClassCastException        |
|      NumberFormatException      |
|             Checked             |
|        SecurityException        |

### 3-2-Checked Exception

|            Exception            |
| :-----------------------------: |
|     ClassNotFoundException      |
|      InterruptedException       |
| StringIndexOutOfBoundsException |
|      NoSuchFieldException       |
|      NoSuchMethodException      |
|     InstantiationException      |
|                                 |

## 4-Exception catching in java

It is a method that allows you to protect the program from any code that you suspect may cause any error using the try and catch statements.

```
try {
    // Protected Code
}
catch(ExceptionType e) {
    // Error Handling Code
}
finally {
    // Optional Cleanup Code
    // Here we write commands to give up anything the program no longer needs
}
```

## 5-Exception class functions in Java

- public String getMessage
- public String toString()
- public void **printStackTrace()**

  - Example :

  ```
  public class Main {

  public static void main(String[] args) {

     String s = "abcd 12345";
     int a;

     try {
         a = Integer.parseInt(s);
     }
     catch( Exception e ) {
         e.printStackTrace();
     }
     }

  }
  ```

  Result :

  ```
  java.lang.NumberFormatException: For input string: "abcd 12345"
  at java.lang.NumberFormatException.forInputString(NumberFormatException.java:65)
  at java.lang.Integer.parseInt(Integer.java:580)
  at java.lang.Integer.parseInt(Integer.java:615)
  at testexceptions.Main.main
  ```

## 6-The throws and throw are in Java

If you define a function and want this function to throw an exception if something specific happens, you have to put the word throws after the parentheses of the parameters and then specify the type of exception that the function may throw.

- Throw : Used to specify the type of exception to be thrown in the catch statement.
- Throws : It is used to specify the type of exception that the function may throw in case you want to test the code and handle it in the place where the function is called.

Exemple 1 : The method used here is called **Exception Thrower/Exception Catcher.**

```
public class Main {

    public static void main(String[] args) {
        checkAge(70);
    }


    public static void checkAge (int age) {
        try {
            if(age > 63) {
                throw new Exception("you are too old!");
            }
        }
        catch( Exception e ) {
            System.out.println( e.getMessage() );
        }
    }

}
```

Exemple 2 : The method used here is called **Exception Thrower/Exception Propagator.**

```
public class Main {

    public static void main(String[] args) {
        try {
            checkAge(70);
        }
        catch( Exception e ) {
            System.out.println( e.getMessage() );
        }
    }

    public static void checkAge (int age) throws Exception{
        if(age > 63) {
            throw new Exception("you are too old!");
        }
    }

}
```

## 7-Create a new Exception and use it in Java

1. A new class that inherits from Exception must be created.

```
public class MyException extends Exception {

    public MyException(String msg){
        super(msg);
    }

}
```

2. The Superclass constructor (ie the Exception constructor) must be called in the new class constructor we are creating.

```
public class Main {

    public static void main(String[] args) {

        try {
            checkAge(20);
            checkAge(18);
            checkAge(10);
        }
        catch( MyException e ) {
            System.out.println( e.getMessage() );
        }

    }


    public static void checkAge(int age) throws MyException {
        if(age < 13) {
            throw new MyException("you can't watch horror movies");
        }
        else {
            System.out.println( "you can watch the movie" );
        }
    }

}
```

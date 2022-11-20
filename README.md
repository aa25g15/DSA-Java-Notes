# DSA Java Notes (Easy To Forget Things)

## Type Conversions

### Integer to String
```java
int i=10;  
String s=Integer.toString(i); // Now it will return "10"  
```

### String to Integer
```java
String s="200";  
int i=Integer.parseInt(s);  // output - 200
```

### Character to Integer
```java
Character.getNumericValue('10'); // output - 10
```

### Uppercase to Lowercase or Vice-Versa
```java
Character.toLowerCase('A'); // output - 'a'
Character.toUpperCase('a'); // output - 'A'
"AbhInaV".toLowerCase(); // output - 'abhinav'
"AbhInaV".toUpperCase(); // output - 'ABHINAV'
```

## Easy to Forget Things And Methods

### To Filter Characters Between 'a' and 'z' Or '0' And '9'
```java
if(ch >= 'a' && ch <= 'z'){
  // Do something
}
if(ch >= '0' && ch <= '9'){
  // Do something
}
```

### Strings are Immutable, Is A Class Not A Primitive Type and Using StringBuilder
Remember that strings are immutable in Java and are not native types but Classes, you have to use StringBuilder class to create mutable character sequence
```java
StringBuilder sb = new StringBuilder(); // Can even mention initial capacity
sb.append("abhinav"); // Unlike many other classes, it is append and not add
sb.append('d');
String result = sb.toString(); // "abhinavd"
```

## Data Structures

### Arrays
```java
String[] = new String[10];
LinkedList<Integer>[] = new LinkedList<Integer>[10]; // XXXXXX Will throw error about generic array creation
```

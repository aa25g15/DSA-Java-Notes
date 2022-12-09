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

### Strings are Immutable, Are Classes And Not Primitive Type and Using StringBuilder
Remember that strings are immutable in Java and are not native types but Classes, you have to use StringBuilder class to create mutable character sequence
```java
StringBuilder sb = new StringBuilder(); // Can even mention initial capacity
sb.append("abhinav"); // Unlike many other classes, it is append and not add
sb.append('d');
String result = sb.toString(); // "abhinavd"
```

### HashSet to ArrayList
```java
HashSet<Integer> solSet = new HashSet<>();
solSet.add(1);
solSet.add(2);
solSet.add(3);
List<Integer> list = new ArrayList<>(solSet);
```

### Arrays.asList Method
```java
import java.util.Arrays;

Arrays.asList(1, 2, 5, 3, 7); // Return a new fixed size List view of the array or arguments passed
```

## Data Structures

### Arrays
```java
String[] = new String[10];
LinkedList<Integer>[] = new LinkedList<Integer>[10]; // XXXXXX Will throw error about generic array creation
```

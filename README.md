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

### Heap poll() method is faster than remove() method for removing the root of the heap

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

### Heaps
```
PriorityQueue minHeap = new PriorityQueue<>(10); // 10 is initial capacity
PriorityQueue maxHeap = new PriorityQueue<>(10, Comparator.reverseOrder());
```

## Deep Stuff

### Stack Overflow And Recursion
@fiwenap423 Stack overflow will only occur when using recursion. You will never get a stack overflow if you're only using an iterative solution.

This is going to be a long answer that covers how the CPU will process a iterative solution and a recursive solution. Understanding what actually happens when your code is run will help build intuition, so here goes:

To illustrate, lets say you have a linked list with n nodes and n = 50000. Well when your solution runs on a physical computer, the nodes for that linked list are stored in memory (RAM).

#### Iteration
When you run your solution, the kernel will execute instructions to
1. Create a program stack in memory (for your program).
2. put the address to function myIterativeSolution at the top of the stack.

The CPU will
1. Fetch the address for: myIterativeSolution and put it in the CPU stack register.
2. go through each instruction, line by line until it hits your while loop.
3. gets a chunk of nodes from memory and loads them into its cache.
4. Runs the instructions in the while loop until it needs a node that isnt in the cache.
5. Clear its cache and goes back to step 4

Finally, when the CPU gets to the end of your function it will
1. pop myIterativeSolution off the program stack
2. remove the address to myIterativeSolution from the CPU stack register and replace it with the address of whatever function called myIterativeSolution.

So from start to finish, this is the stack
```java
// push program entry function
[main()]

// push iterative solution when called
[main(), myIterativeSolution()]
// ... process all nodes until it gets to the end of the function ...

// pop iterative solution when complete
[main()]

// exit program when stack is empty
[]
```

#### Recursion
With a recursive solution, the CPU will do everything as before, but it may never reach the end of the function. It could just repeat these steps.

1. push that onto the program stack
2. load it into stack register
3. keep reading instructions
4. see myRescursiveSolution() function call and go back to step 1.

So the program stack looks like this in memory:
```java
// push program entry function
[main()]
// keep pushing `myRecursiveSolution` onto the stack whenever a stack frame calls that function.
[main(), myRecursiveSolution()]
[main(), myRecursiveSolution(), myRecursiveSolution() ]
[main(), myRecursiveSolution(), myRecursiveSolution(), myRecursiveSolution(), ]
[main(), myRecursiveSolution(), myRecursiveSolution(), myRecursiveSolution(), ... 5000 calls later... myRecursiveSolution(),] // <--- cant do this, no space

// ERROR! program runs out of stack memory and exits.
```

#### Conclusion
When running programs you're always using a program stack in memory. If you're solution doesn't use recursion, you don't have to add this to the cost of the solution. But if it does, then you have to consider the input size or use tail end recursion (or trampoline recursion).

But if you use iteration, and don't allocate something new with each iteration, then your space complexity is O(1). Because each iteration will have upto the amount of data you can store in CPU cache.

Cache examples with n = 50000:

cache capacity	round trips to complete
50 nodes	1000
500 nodes	100
5000 nodes	10
With a cache that fits 500 nodes at a time, it doesn't matter what n is. Each round trip fetches 500 nodes. The space complexity will always be constant: exactly O(500) or generally O(1).

#### Recursion warning
Recursion is used for simplicity and readability. Sometimes it can really make a solution succinct and understandable. You should never use it if you want speed, because the CPU and MMC (the middle man between CPU and RAM) are going to be doing way more work.

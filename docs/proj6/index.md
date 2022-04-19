# COMP 241 Project 6

## Dijkstra's algorithm

[💾 **Download starter code**](proj6-starter.zip)

In this project, we will put all of our pieces from this semester together.  Well, at least some of them.  You will write a program implementing a classic algorithm, picking the best data structures to use in the code.  You will also get experience using some built-in Java data structures we haven't used yet.

### Primer on the Java Collection Framework

For this project, you will be using a number of classes in the Java Collections Framework, which contains all of the basic data structures programmers commonly use in their programs, including a variety of Lists, Sets, and Maps.  You have already used ArrayLists, LinkedLists, and HashSets in previous projects; for this project, you will make use of the built-in Java Maps, known as HashMap (implemented with hash tables) and TreeMap (implemented with a variety of a BST).  If you are not already familiar with these, [you can read this description of how they work](java-collections.html).

### Project description

You will implement Dijkstra's algorithm for this project.  Your project will read in a description of a graph from a file, which may be directed or undirected, and then run Dijkstra's algorithm to compute the shortest path between two vertices specified in the file.

To make your life easier, the graph data structure and priority queue data structure are already written for you.  Read about the [graph](graph.html) and the [priority queue](pq-class.html) classes.

### Part A: File Reading

Each file describes a graph.  Take a look at the examples given in the `src` folder (graph1-graph4).  You should be able to see how the file structure works.  There are four possible commands you’ll see in these files: 

- The first line of the file will always be the word `directed` or `undirected` which specifies the type of graph. To make your life easier, this project just “fakes” undirected graphs as directed graphs where each edge is duplicated for the two directions. 
- `vertex name`: this command adds a vertex called `name` to the graph. You may assume `name` is a string that hasn’t already been used as the name of a vertex.
- `edge name1 name2 weight`: this command adds an edge between the vertices `name1` and `name2` with the given integer weight. You may assume `name1` and `name2` have already been added to the graph, and there is not an existing edge between them already. 
- `dijkstra name1 name2`: this command will always be the last one in the file. When your program sees this command, your code should print out a list of all the vertices and edges in the graph (see the sample output for the formatting).  Then your code calls your Dijkstra’s Algorithm function (see below) to find the shortest path from vertex `name1` to vertex `name2`. (Note that up to this point, you don’t have to write or change any code.)

**Completing Part A**

To write Part A, fill in the `processFile` function.  Follow the model we've used in previous projects.  

A few hints, tips, and guidelines:

- Notice a `Graph g` is already created for you.
- I suggest using a series of if/else if/else tests to check which category from above `words[0]` falls into.  Then call `g.addVertex()` or `g.addEdge()` as appropriate.  
- The `Integer.parseInt()` function will turn a `String` into an `int`.
- For `directed`/`undirected`, you'll need some way of saving this piece of information so you know whether to add two edges or just one.
- For now, since you haven't written the Dijkstra's algorithm function, when you read the `dijkstra` command from the file, you should print all the vertices and edges, but you won't be able to call the `dijkstra()` function (or you can call it, but it won't do anything, because it's mostly empty now).

**Debugging Part A**

- If you run into problems, use lots of print statements.  You can print the entire state of the graph with `System.out.println(g)`.  This is handy to see what your graph looks like.

**How do I know when Part A works?**

When your output from the list of vertices and list of edges for each graph matches mine (see the output section below), you should feel confident that you're ready to move on.

### Part B: Dijkstra's algorithm

In this part, you will implement Dijkstra's algorithm, which we discussed in class.  [Here's the pseudocode](https://rhodes.app.box.com/s/k08g32b1stbec2mn93r7l0xoho3zbcmt).

**Completing Part B**

- First, you will need to pick your data structures.  There are three major data structures in the algorithm, namely `dist`, `prev`, and the priority queue, which has already been created for you.  `dist` and `prev` are maps: `dist` keeps track of the best distance so far for each vertex, so it is a map from `String`s to `int`s.  `prev` keeps track of the best "previous" vertex for each vertex in the graph, so it is a map from `String`s to `String`s.  (Recall that vertices in our graph are represented as strings.)

  What you need to do is decide whether to use a `HashMap` or a `TreeMap` for each of these maps.  Which would be better here?  Using a hash table or a binary search tree?  (Either will work fine, but you should think about this.)

- Next, translate the pseudocode into Java code.  Unlike some previous projects, this code cannot be cut-and-pasted; you will need to think about how each line should be expressed in Java.  Refer back to the details of the [graph class](graph-class.html) and the [priority queue class](pq-class.html), and how [Java Maps](java-collections.html) work.

- Your code *must* output each vertex as it is visited (removed from the priority queue), and it also *must* report all changes to the `dist` map.  I suggest, however, using additional print statements to help debug.  What I did was I made a `DEBUG` constant that triggers extra output when it's set to `true`.  See my sample output below for examples of this.

- At the end of the algorithm, your code *must* print four pieces of information:

  - The final shortest path.
  - The distance of that shortest path.
  - The contents of the final `dist` map.
  - The contents of the final `prev` map.

**Debugging Part B**

- If you run into problems, use print statements to print every step of the algorithm as it is being completed.  See my sample debugging output for ideas.

**How do I know when Part B works?**

When your output from the list of vertices and list of edges for each graph matches mine (see the output section below), you should feel confident that you're ready to move on.

### ✅✅✅ Sample output

I will be checking your output against the "without debugging" output.  Everything should match, with the exception of:

- The order of the vertices and edges listed at the beginning (when you just print the contents of the graph).
- The order in which the *neighboring* vertices `v` of each vertex `u` are considered during each step of the algorithm (e.g., if vertex A is connected to vertices B and C, your algorithm may consider B before C, or C before B).  To be clear, the order of the `u` vertices (being removed from the priority queue) must match.  The order of the `v` vertices *within* each iteration of the main loop does not matter.
- and the order of the vertices in the `prev` and `dist` maps printed at the very end.

**Files**

- `graph1.txt`: [without debugging](graph1-output.txt) | [with debugging](graph1-output-debug.txt)
- `graph2.txt`: [without debugging](graph2-output.txt) | [with debugging](graph2-output-debug.txt)
- `graph3.txt`: [without debugging](graph3-output.txt) | [with debugging](graph3-output-debug.txt)
- `graph4.txt`: [without debugging](graph4-output.txt) | [with debugging](graph4-output-debug.txt)

### Turning in the project

Upload `DijkstrasAlgorithm.java`.  No other files are needed.

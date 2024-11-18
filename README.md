# MatrixGraphBuilder
**A generic collection to turn a 2D matrix into its graph**

## Introduction
This project aims to create a free public generic collection to convert any 2D matrix type into its graph, in other terms, you can create any matrix `T[n,m]` of type `T`, width `n` and height `m`. 
This implementation has a time complexity of `O(n*m)` due to the need of iterating over every elements of the matrix and has a space complexity of `O(n*m)` as well as we need to store every elements of the matrix as a key in the adjacency matrix.

For conditions of utilization, please refer to the [LICENSE](https://github.com/jojo2504/MatrixGraphBuilder/blob/main/LICENSE).

## Installation and Usage
To use the project, simply download the `MatrixGraphBuilder.cs` or clone/add submodule the repository.
Then to use the class:
```csharp
MatrixGraphBuilder<char> graph = new MatrixGraphBuilder<char>(); // non init matrix
MatrixGraphBuilder<char> graph = new MatrixGraphBuilder<char>(new char[,]{{'a', 'b'},{'c', 'd'}});
```

## Implementation method
The class iterates through every elements of the matrix and then iterates around it the create neighbors. Using a `Dictionary<Node<T>, HashSet<Node<T>>>?`, it stores each element of the matrix as a key and add every of its neightbors in the `HashSet<Node<T>>`.

The graph uses a struct struct `Node<T>` which has as values : `Value, Row, Col` to keep track of each node position in the graph to avoid duplicate keys/values in the `Dictionary<Node<T>, HashSet<Node<T>>>`.
```csharp
public readonly struct Node<T>{
  [...]
  public Node(T value, int row, int col){
      Value = value;
      Row = row;
      Col = col;
  }
}
```
## Additionaly
You can use these additional provided methods for update and debug purpose:
```csharp
public void SetMatrix(T[,] matrix)  // set new matrix to convert
public void Clear()                 // clear the current graph
public override string ToString()   // returns a string which nicely represent the adjacency matrix of the graph
```

## Exemple
Here is a small provided example of how to use this class.
```csharp
MatrixGraphBuilder<char> graph = new MatrixGraphBuilder<char>(new char[,]{{'a', 'b'},{'c', 'd'}});
Console.WriteLine(graph.ToString());
/// a(0,0) => b(0,1), c(1,0)
/// b(0,1) => a(0,0), d(1,1)
/// c(1,0) => a(0,0), d(1,1)
/// d(1,1) => b(0,1), c(1,0)

graph.Clear()

graph.SetMatrix(new char[,]{{'a'},{'c'})
Console.WriteLine(graph.ToString());
/// a(0,0) => c(1,0)
/// c(1,0) => a(0,0)
```




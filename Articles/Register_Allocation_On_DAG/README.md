# Register Allocation On DAG

Register allocation happens when a DAG (directed acyclic graph) that represents an execution flow is being serialized.

Let's look at the example function below, assuming that all operations are just arithmetic operations on integers.

## Example: `a, b -> (a + b) * (-b)`

This function takes `a` and `b` as input parameters and outputs the result of `(a + b) * (-b)`, whose execution flow can be represented by the following DAG:

![](example-dag.png)

There are two possible ways of sequentially doing the calculation, one is to compute `+` first, and the other is to compute `-` first, as the animations below show. Note that once a computed value is no longer in use, the space it occupies can be freed up.

![](example-order-1.gif)

![](example-order-2.gif)

Although they will eventually produce the same result, their runtime space costs are different. The first way only requires at most two intermediate results to be stored at the same time, while the second way requires three.

## The Optimal Register Allocation Problem On DAG

With a given DAG, we define two possible states of a vertex: `Inactive` and `Active`.

At the beginning, only the vertices without predecessors are `Active`, which means they already contain values, while all other vertices are `Inactive` and are to be evaluated.

For each step, we choose one `Inactive` vertex whose all predecessors are `Active` and evaluate it, turning it to `Active`. At the same time, we check if there is any predecessor of this vertex whose all descendants are by now `Active`, and convert all of them back to `Inactive` to free up their spaces.

The problem is, how to choose the order in which the vertices are to be evaluated, so that the maximum number of vertices that are in `Active` state at the same time is minimized.

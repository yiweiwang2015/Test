# Class Scheduling
## Introduction
- This program is aimed at finding a valid order of courses to take that each of the courses is taken after all the prerequisites are satisfied.
- The input is a path to a JSON file containing class names and all the prerequisites associated.
<br />Example:
<pre> 
[
    {
        "name": "Algebra 1",
        "prerequisites": []
    },
    {
        "name": "Geometry",
        "prerequisites": []
    },
    {
        "name": "Algebra 2",
        "prerequisites": ["Algebra 1", "Geometry"]
    },
    {
        "name": "Pre Calculus",
        "prerequisites": ["Algebra 2"]
    }
]
</pre>
- The output is a valid order of classes based on which students can take their courses. The order is printed out in the format that one class name is printed per line. If there is no valid order exits or the program runs into errors, an error message will be printed out.
## Specification
This program is written in Java, please use IntelliJ IDEA to build the exicutable.
## Algorithm
- Idea: 
<br />Use topological sort based on node indegree to find a valid class schedule, which can be considered as a topological order. Imagine every course as a node in a directed graph, only nodes with 0 indegree (means no prerequisites) can be taken first.If we remove all these courses from the graph, along with their outgoing edges, we can find out the courses/nodes that should be processed next. These would again be the nodes with 0 indegree. We can continuously do this until all the courses have been accounted for.
- Algorithm:
<br />1. Read Json file and iterate over all the edges in the input. Create an adjacency list for each course and map the list to the course in a HashMap. Store the indegree of each course in another map.
<br />2. Initialize a queue to keep a track of all the nodes with 0 indegree. Add all the nodes with 0 indegree to the queue.
<br />3. The following steps are to be done until the queue becomes empty:
  <pre> 
  1. Pop a node from the queue. Let's call this node N.
  2. For all the neighbors of this node N, reduce their indegree by 1. If any of the nodes' indegree reaches 0, add it to          the queue.
  3. Add the name of node N to the result stringbuilder maintaining topologically sorted order.
  4. Continue from step 3.1.
  </pre>
- Performance Analysis: 
<br />Time Complexity: O(n*m), where n is the number of courses and m is the maximum number of prerequisites for a class, since we process each entry (class and its prerequisites) in the Json file exactly once and for each entry we also process every class in its prerequisites exactly once.


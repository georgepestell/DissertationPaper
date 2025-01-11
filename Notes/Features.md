The cost algorithm's fundamental goal is to rank routes from a source point to an end point, given a history of previous cost calculations leading to that point. There are, in fact, many different ways we can rank routes across a terrain including energy exerted, perceived difficulty, or time taken. 

The cost function is customisable, with a set of data features, and a set of functional features. Features can accept input from the output of other features as dependencies, creating a directed acyclic graph (DAG) dependency tree. Dependencies represent data dependencies to calculate the value of a Feature for a particular section of a route.

A DAG graph structure enforces the following characteristics onto the cost function. First, dependencies of a feature are directed, meaning $\textbf{D}_A = \set{B} \neq \textbf{D}_B = \set{A}$ dependants are aware of their dependencies, but dependencies are independent of their dependents. This prevents features from having access they shouldn't have access to, reducing the likelihood of introducing errors when creating new features. Next, the cost function acyclic, meaning no child of a Feature $A$ depends upon a feature 

directed meaning dependencies are one-way dependencies, where the dependency does not depend on the dependent; acyclic meaning that any dependency $d_{Ax}$ of a feature $A$ cannot be dependent on any feature

The  and Feature classes is such that the cost function maintains the structure of a directed acyclic graph, where features have dependencies, but no subsequent child of a feature depends upon any of it's ancestors (preventing infinite dependency loops).

The provided presets give examples of time as the primary model for the cost. However, the cost algorithm is designed to be used as a framework for which further research can be utilized, allowing any quantifyable feature to represent the cost.


For the cost function pre-sets provided, the total time was chosen as the primary factor in determining the cost, as modelling this takes into consideration the speed and distance covered. 

Many factors influence the speed an individual will travel over a particular section of the terrain. The presets given make a first attempt at quantifying these factors together to build a full model predicting walking speed. Further research into these factors and their interactions with each other would likely lead to a strong improvement in the quality of the routes generated.

Some factors influence speed in a more psychological way. For example, walking on a flat surface will often be significantly slower when there is a sudden large fall visible alongside the road, such as walking next to a cliff-edge. Here, the fear of falling causes a reduction in walking speed.


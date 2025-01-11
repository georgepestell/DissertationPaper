The routing algorithm is designed to minimize or maximize a configurable cost function.

The presets that have been created as exemplars of some of the capabilities this system have aim to minimize the estimated overall cost of the route.

The cost function is calculated by calling `calculateCost` on the `FeatureManager` object. This object stores the root output feature. The feature manager calls the `calculate` function for this feature, which in-turn can make function calls to dependent features, forming a DAG.

The calculateCost function calculates the cost to travel from the current node to an adjancent node.
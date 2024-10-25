# Smartflow
SmartFlow Decision Science: Optimizing Multi-Modal Transportation for Cost-Efficient Supply Chains 

# MultiModal Transport Optimization Documentation

## 1. Introduction

The `MultiModalTransportOptimizer` class is designed to find the most cost-effective way to transport goods between different cities based on user-defined routes and orders. The optimization uses linear programming to minimize transportation costs while fulfilling all orders.

## 2. Assumptions

1. **Routes and Costs**: It is assumed that all routes provided by the user have defined costs. There are no routes with undefined costs.
2. **Demand Fulfillment**: The model assumes that the sum of goods ordered does not exceed the supply available from the defined routes.
3. **Non-negativity**: The amounts transported along the routes are non-negative. It is not possible to transport negative quantities.
4. **Fixed Routes**: The routes and their associated costs are fixed and do not change during the execution of the program.
5. **Discrete Cities**: The list of cities is predefined and the user selects from this list; no new cities can be added dynamically.

## 3. Decision Variables

The decision variables in this optimization model represent the amount transported between each origin and destination. They are defined as follows:

- **x[i, j]**: Amount transported from origin `i` to destination `j`, where `i` represents the index of the origin city and `j` represents the index of the destination city.

## 4. Parameters

The parameters for the model include:

1. **Routes**: A dictionary containing the transportation routes between cities and their costs.
   - Example: `routes = {("New York", "Los Angeles"): 10, ("Chicago", "Houston"): 15}`

2. **Orders**: A dictionary containing the order quantities required at each destination city.
   - Example: `orders = {"Los Angeles": 30, "Houston": 50}`

3. **Cost Matrix**: A matrix that holds the costs associated with each route from origins to destinations, derived from the `routes` parameter.

## 5. Mathematical Modeling

### Objective Function

The objective of the optimization model is to minimize the total transportation cost:

\[
\text{Minimize} \quad Z = \sum_{i=1}^{m} \sum_{j=1}^{n} c_{ij} \cdot x_{ij}
\]

Where:
- \(Z\) = Total transportation cost
- \(c_{ij}\) = Cost of transporting goods from origin \(i\) to destination \(j\)
- \(x_{ij}\) = Amount transported from origin \(i\) to destination \(j\)

### Constraints

1. **Supply Constraints**: The total shipment from each origin should not exceed the total supply available. Here, we assume that the total capacity is equal to the sum of the orders.
   \[
   \sum_{j=1}^{n} x_{ij} \leq \text{Total Supply} \quad \forall i
   \]

2. **Demand Constraints**: The total shipment to each destination must meet the order quantity.
   \[
   \sum_{i=1}^{m} x_{ij} = \text{Order Quantity at Destination} \quad \forall j
   \]

Where:
- \(m\) = Number of origins
- \(n\) = Number of destinations

## 6. Results

The optimization problem is solved using the CVXPY library, which provides the necessary tools to model and solve linear programming problems. After running the `solve()` method, the program outputs the optimal transportation plan that specifies how much to transport along each route, achieving the lowest possible cost while satisfying all demands.

### Example Output

Upon successful execution, the program will display:

- The routes defined by the user, along with their costs.
- The order quantities for each destination.
- A statement summarizing the optimized transportation plan.

**Sample output**:
Optimal solution found: You selected the following routes: From New York to Los Angeles at a cost of $10. From Chicago to Houston at a cost of $15.

You have ordered the following quantities: 30 units to be sent to Los Angeles. 50 units to be sent to Houston.

The program has optimized the transportation plan. This means that it found the best way to send goods from different cities to other cities while spending the least amount of money.


### Conclusion

The `MultiModalTransportOptimizer` effectively optimizes the transportation process for multiple orders across predefined routes, ensuring that logistical needs are met at minimal costs. The model can be easily adapted for more complex constraints and larger datasets by extending the parameters and constraints defined.

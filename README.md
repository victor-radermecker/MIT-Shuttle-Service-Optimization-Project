# MIT Shuttle Service Optimization Project

MIT offers a shuttle service to its community members, connecting different locations on campus. The current service operates as a traditional public bus, following the same route throughout the day, picking up and dropping off people at their preferred bus stop. However, the shuttle is currently underused due to unreliable bus schedules, long riding times, and little flexibility in the stops. As a result, it often runs empty, wasting resources like fuel and emitting unnecessary CO2.

`Authors:` Marco Antonioli, Victor Radermecker
`Professors:` Prof. Jacquillat

## Objective

The aim of this project is to optimize the shuttle's route to better service each customer's needs. We have increased the number of possible stops from 13 to 45, covering the entire MIT area with strategic locations, including undergrad/grad residences, main MIT buildings, shops, and more. Our model takes each customer's request as an Origin-Destination (OD) pair and optimizes the total route. By offering a customized service, we can precisely meet the demand, avoiding the waste of precious resources.

## Route Optimization Model

To achieve this objective, we have implemented two versions of the Dial a Ride Problem (DARP): a three-index formulation and a two-index formulation. The constraints for the three-index formulation are as follows:

```math
\min_{x} \quad \sum_{k \in K} \sum_{i \in V} \sum_{j \in V} x^{k}_{ij}c^{k}_{ij}
```

Subject to:

- Constraints for pickups and drop-offs at each stop
- Constraints for pickups and drop-offs at the depot
- Constraints ensuring each customer is served properly
- Constraints ensuring the shuttle operates within its time windows and capacity limits
- Binary constraints for decision variables

For a detailed mathematical representation, refer to the equation in the project report.

## Implementation Details

For our implementation, we considered a randomly selected point from a residence as the origin and a randomly selected point from all other points of interest as the destination. The data required for the model was generated following the process described in the "Data" chapter of the report.

## Implementation Challenges

The main challenge in implementing the optimization model lies in its scalability to a large number of passengers, primarily due to small preference time windows for each customer and the exponential growth of binary variables with the number of passengers. To address this, we have made the following optimizations:

### Adding Penalty on Non-Respected Time Windows

We have allowed the shuttle to violate preferred time windows slightly, introducing a penalty on the objective function for every violated time window. This allows us to linearize the new objective function and make the problem more feasible for a larger number of customers.

### Graph Preprocessing

Since not all edges are relevant due to time windows and precedence constraints, we have reduced the number of variables in the final formulation by removing infeasible edges. Additionally, we have implemented tighter time window constraints on the depot nodes, further improving the model's efficiency.

## Conclusion

Through our optimized route optimization model, we believe the MIT shuttle service can significantly improve its efficiency, offering a customized service that better meets the demand while minimizing resource waste. The implementation challenges have been addressed to ensure the model's scalability, allowing for potential future expansion with a larger number of passengers.

For more details on the implementation and results, please refer to the full project report.

*Note: This README provides an overview of the project. For a complete understanding, kindly refer to the project report in its entirety.*


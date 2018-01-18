# Summary
This project implements the simulation of an elevator. Different strategies for picking up and dropping off passengers were tested with the goal of minimizing the 95th percentile simulated travel time. The 95th percentile was chosen as the metric to minimize as opposed to just the average as minimizing the average may have led to a strategy that worked extremely well for passengers on lower floors, but almost totally failed for passengers on top floors of the building.

# Strategies and Efficiency
In this simulation, three elevator passenger carrying strategies are implemented. The first has the elevator starting on the ground floor and moving all the way to the top floor, stopping at every floor in between. When it reaches the top floor, the elevator changes direction and moves all the way back down to the ground floor, again stopping at every floor in between. Passengers are picked up and dropped off at their destinations as space permits. This strategy was implemented in the example_strategy_step_function() function which does not actually move the elevator, but rather returns an action for the Simulation class. This action tells the elevator whether to move up, down, or stop and open its doors. All the strategy functions operate in this fashion, returning only commands to the elevator for the next time step, leaving it to the Simulation class to calculate the time each passenger spends in transit, and “moving” the elevator. This strategy is used as the baseline strategy.

In the second strategy, a “First Come, First Serve” transit style strategy is adopted wherein the first person to request the elevator is picked up, and taken to their destination, before new passengers are picked up. This strategy could be further optimized by picking up passengers while the elevator is on the way to a starting floor as opposed to skipping over those passengers. Additionally, the simulation does not actually incorporate time steps into when passengers are requesting the elevator; all passengers are initialized in a single loop, and each passenger is initialized with a starting floor, and destination floor. However, each person and their destination floor is appended to a list, and their index in that list is treated as the order in which they request the elevator.

In the third strategy, named the democratic_step_function(), an elevator strategy that serves the people is devised. The strategy applies the logic that while the elevator is moving, if a passenger reaches their destination, they get out. If the elevator is moving and people are waiting on a floor it is moving past, it picks them up. With these people in, it travels to the floor that the most people in the elevator want to go to. If no people are in the elevator, it goes to the floor that the most people are waiting on. We understand that this strategy would be difficultly to implement with standard elevator hardware, but wanted to develop the most efficient strategy possible given these constraints.

# Efficiency
In determining the efficiency of the implementations, there were a number of possible metrics to consider. Expected wait time before entry, maximum wait time before entry, the quality of service (the expected number of people whose wait time is substantially larger than the expected wait time), and the energy used are all metrics that should be considered if searching for the truly optimal elevator strategy. To determine the “best” strategy, the average number of extra steps each passenger took was observed. An extra step is calculated by looking at the number of floors between a passenger’s starting point and ending point, and subtracting that number from the number of steps they actually took.

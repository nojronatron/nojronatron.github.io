# Partner Power Hour - Graphs and Navigation App

Speaker: Roger R

Codefellows Alum and current Java TA

## Dijkstra's Algorithm

Used to find shortest path from starting location to a destination.

Based on a Graph datastructure.

## Demo

Hashmap: Key-value pairs structure. In this case: Keys of Cities, and a collection of values (roads with time to travel).

Edges are bi-directional in this graph.

Stored Info class: Stores KVPs City:TravelDetails.

Inputs include:

- Multiple Cities, based on Class created (constructor takes a city name).
- New State, with Cities added.
- Roads with travel times between cities.

NavPrompt Class:

- Helps navigate the Graph
- Execute the Dykstra Algorithm

Dijkstra Class:

- Code heavy.
- Start at first City (a Graph Node).
- Add to Cities to Check collection, and store the totalTravelTime to 0.
- Remove from Cities to Check and add to CurrentLocation.
- Check connected Roads and their connected Cities, comparing against Completed Cities (already checked).
- Add travelTime to the totalTravelTime if not in CompletedCities, and check if it is less than MAX, and update the Path Collection with the Current Location (City).
- Continue with the next road, as in the previous step.

## Notes

When comparing for the 'least distance' or a minimum value, it was imporant to start the existing value at MAX_VALUE to simplify comparisons.

If travel times between the same two cities in opposing directions are not the same, utilize bidirectional Edge properties in the Graph.

## Footer

Return to [pph index](./pph-index.html)

Return to [root README](../README.html)

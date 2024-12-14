# Advent of Code 2024
Read about Advent of Code here -> [Link](https://adventofcode.com/)

# Day 14
Part two of the Day 14 problem involved finding a hidden Christmas tree, represented by robots moving in a 2D space. 
This challenge introduces some interesting applications of entropy, which are worth exploring further. 

That is how random the robots are in each iteration. 

And to further explain: The Christmas tree is visible after x seconds in the grid (width 101 and height 103) of robots moving.

Both solutions make the assumption that when the Christmas tree is visible, the robots/points are tightly grouped 
and not randomly spread out. This means the entropy is at its minimum.

Both solutions below work but number two is much more expensive to compute.

## First solution 
Find the minimum average distance to the center point of the grid over all one-second iterations.

The minimum average distance to the center point (xm,ym) was 31.3, and found 7037 iterations into the simulation.

```python
# Calculate the average distance to mid point
# xm = mid point x
# ym = mid point y
vg_distance = sum(abs(px-xm) + abs(py-ym) for px,py in result) / len(result)
```


## Second solution
Find the minimum of the average distance between the different points over all one-second iterations.

The time and cost of computing this is very high. In total, about 45 seconds to iterate over all possible positions.

The minimum average distance between points was 30.6, found at 7037 iterations into the simulation.

```python
points = np.array(points)
    n = len(points)

    # Calculate pairwise distances
    distances = np.sqrt(((points[:, None, :] - points[None, :, :]) ** 2).sum(axis=-1))
    pairwise_distances = distances[np.triu_indices(n, k=1)]

    # Calculate the average distance
    average_distance = pairwise_distances.mean()
```

# Conclusions - By GPT4o 

The analysis of the robot movements in this simulation highlights the usefulness of entropy in identifying patterns. By assuming that the Christmas tree becomes visible when the points are tightly grouped (minimum entropy), we developed two methods to quantify this behavior.

- **First Solution:** By measuring the average distance to the center point, we found a computationally efficient method to identify the time at which the robots are most clustered. This approach provides a good approximation with relatively low computational cost.

- **Second Solution:** By calculating the average pairwise distances, we obtained a more precise measure of clustering. However, this approach is significantly more computationally expensive, taking about 45 seconds for the entire simulation.

In conclusion, while the second solution offers higher accuracy, the first solution is a practical and efficient alternative for larger simulations. Both methods effectively demonstrate how entropy can be minimized to detect patterns in spatial distributions.

# Traveling Salesman City-Tour Optimizer

This project solves a variation of the **Traveling Salesman Problem (TSP)**, which determines the most efficient route for visiting multiple cities and returning to the starting city. The project implements several algorithms to optimize the tour, including a **Greedy Algorithm**, **2-opt Algorithm**, and **Simulated Annealing**. It reads city data from a CSV file, calculates distances between cities using the **Haversine formula**, and provides an interactive solution through a command-line interface (CLI).

---

## Features

* **CSV Parsing**: Read cities and coordinates from a CSV file.
* **Distance Calculation**: Calculate distances between cities using the **Haversine formula** (great-circle distance).
* **TSP Solvers**: Choose between multiple algorithms to solve the Traveling Salesman Problem:

  * Greedy Algorithm
  * 2-opt Optimization Algorithm
  * Simulated Annealing
* **GeoJSON Output**: After computing the optimal route, a **GeoJSON** file is generated for map visualization.
* **Command-Line Interface**: A CLI to input parameters such as the start city, algorithm choice, and the number of cities to limit for quicker computation.
* **Route Plotting**: Plot the route using **matplotlib** for visualizing the city tour.

---

## Table of Contents

1. [Installation](#installation)
2. [Project Structure](#project-structure)
3. [How to Run](#how-to-run)
4. [Command-Line Arguments](#command-line-arguments)
5. [Expected Output](#expected-output)
6. [GeoJSON Export](#geojson-export)
7. [Algorithms](#algorithms)
8. [Example Use Case](#example-use-case)
9. [License](#license)
10. [Contributing](#contributing)

---

## Installation

1. Clone this repository to your local machine:

   ```bash
   git clone https://github.com/yourusername/tsp_city_tour_optimizer.git
   cd tsp_city_tour_optimizer
   ```

2. Install the required dependencies:

   ```bash
   pip install -r requirements.txt
   ```

   The `requirements.txt` file includes the necessary Python libraries such as `argparse`, `math`, `json`, and `matplotlib` for plotting.

---

## Project Structure

The project is organized into several Python files and a CSV file:

### 1. **`tsp.py`**:

* This is the main script that runs the Traveling Salesman Problem (TSP) solver.
* It handles the **command-line interface (CLI)** and processes input arguments.
* It also reads the city data from the CSV file, applies the selected algorithm, and generates the results.
* **Key functions**:

  * Handles command-line arguments.
  * Reads the CSV file containing city data.
  * Runs the selected algorithm (Greedy, 2-opt, or Simulated Annealing).
  * Outputs results to the console and generates the route in GeoJSON format.

### 2. **`tsp_solver.py`**:

* This file contains the implementation of different TSP-solving algorithms:

  * **Greedy Algorithm**: A simple, fast method that chooses the nearest unvisited city at each step.
  * **2-opt Algorithm**: An optimization technique that swaps two edges of the route to reduce the overall distance.
  * **Simulated Annealing**: A probabilistic algorithm that allows occasional "bad" moves to escape local minima and explore better solutions.

### 3. **`places.csv`**:

* This is a sample CSV file containing city names and their latitude and longitude coordinates.

* The format of the CSV is as follows:

  | City Name    | Latitude | Longitude |
  | ------------ | -------- | --------- |
  | Eiffel Tower | 48.8584  | 2.2945    |
  | Place 2      | 48.8647  | 2.2968    |
  | Place 3      | 48.8629  | 2.2903    |
  | ...          | ...      | ...       |

* The cities in this file will be used as the cities to optimize the travel route.

### 4. **`plot_route.py`**:

* This file is responsible for visualizing the optimal route on a map.
* **Key functions**:

  * Uses `matplotlib` to plot the cities and the optimal route.
  * Reads the GeoJSON file generated by the TSP solver and plots the route on a 2D plane.
  * Displays the city locations and the path between them.

### 5. **`requirements.txt`**:

* This file contains the list of Python packages required for the project to run. The dependencies include:

  * `argparse` for command-line argument parsing.
  * `math` for mathematical functions.
  * `json` for working with JSON files (GeoJSON in this case).
  * `matplotlib` for plotting the optimal route on a map.
  * `numpy` for numerical operations (if required by some algorithms).

### 6. **`route.geojson`**:

* This is the output file that stores the optimal travel route in **GeoJSON** format.
* This file is used for visualizing the route in a mapping tool like Google Maps or geojson.io.
* After running the algorithm, this file will be generated, containing the city coordinates and the optimal travel path.

### 7. **`Distance.py`**:

* This file contains the logic for calculating the **Haversine distance** between two cities, based on their latitude and longitude coordinates.
* **Key functions**:

  * **`haversine_distance(lat1, lon1, lat2, lon2)`**: Computes the great-circle distance between two points on the Earth's surface given their latitude and longitude.

### Example of `Distance.py` Function:

```python
from math import radians, sin, cos, sqrt, atan2

def haversine_distance(lat1, lon1, lat2, lon2):
    # Convert latitude and longitude from degrees to radians
    lat1, lon1, lat2, lon2 = map(radians, [lat1, lon1, lat2, lon2])
    
    # Haversine formula to calculate the great-circle distance
    dlat = lat2 - lat1
    dlon = lon2 - lon1
    a = sin(dlat / 2) ** 2 + cos(lat1) * cos(lat2) * sin(dlon / 2) ** 2
    c = 2 * atan2(sqrt(a), sqrt(1 - a))
    R = 6371  # Radius of the Earth in kilometers
    return R * c  # Distance in kilometers
```

---

## How to Run

### Step 1: Prepare the CSV File

Ensure that the cities and their coordinates are properly stored in a CSV file (`places.csv`).

### Step 2: Run the Script

You can run the script from the command line with the following syntax:

```bash
python tsp.py --csv <CSV_FILE> --start "<START_LOCATION>" --<OTHER_OPTIONS>
```

### Command-Line Arguments

These arguments can be passed to customize how the program runs:

* **`--csv`**: Path to the CSV file containing city names and coordinates (e.g., `places.csv`).
* **`--start`**: The city name from which the tour should begin (e.g., `"Place 1"`).
* **`--limit`**: (Optional) Limits the number of cities for faster testing. Default is `None`.
* **`--algo`**: Algorithm to solve the TSP. Choose from:

  * `greedy`: Uses the **Greedy** algorithm (default).
  * `2opt`: Uses the **2-opt** algorithm for optimization.
  * `simulated-annealing`: Uses the **Simulated Annealing** algorithm.
* **`--should-return`**: (Optional) If provided, the algorithm will ensure the tour returns to the starting city after visiting all cities.

---

## Expected Output

After running the script, you will get the following outputs:

1. **Optimal Tour**: A list of cities in the optimal order (printed in the console).
2. **Total Distance**: The total distance of the optimal tour in kilometers.
3. **GeoJSON File**: A `route.geojson` file that you can visualize in a mapping tool like Google Maps.

### Example Output:

```
Optimal tour:
1) Place 1
2) Place 3
3) Eiffel Tower
...
Total distance: 120.32 km
Route written to route.geojson
```

The `route.geojson` will contain the optimal route with the coordinates of each city, ready to be viewed in a map visualization tool.

---

## GeoJSON Export

The script generates a `route.geojson` file after computing the optimal route. This file can be used to visualize the city tour on a map.

Here’s an example of how to view the route in **Google Maps**:

1. Go to [geojson.io](http://geojson.io/).
2. Click on **"Open"** and upload the `route.geojson` file.
3. The route will be displayed on the map.

---

## Algorithms

The project implements three TSP-solving algorithms:

### 1. **Greedy Algorithm**

The Greedy Algorithm starts from a given city and iteratively picks the nearest unvisited city. This approach is fast but does not guarantee an optimal result. It is useful when speed is more important than perfection.

### 2. **2-opt Algorithm**

The 2-opt Algorithm improves upon the Greedy approach by performing swaps on two edges of the route. If the swap results in a shorter path, it is kept. This method can lead to better solutions but requires more computation time than the Greedy Algorithm.

### 3. **Simulated Annealing**

Simulated Annealing is a probabilistic algorithm that allows "bad" moves (i.e., moves that increase the total distance) to escape local minima. Over time, the probability of accepting worse moves decreases, which helps the algorithm converge to an optimal or near-optimal solution.

---

## Example Use Case

Here’s an example where we want to find the optimal city tour starting from **"Place 1"**, using the **2-opt algorithm**, and limiting the number of cities to 50:

```bash
python tsp.py --csv places.csv --start "Place 1" --limit 50 --algo 2opt --should-return
```

This will:

* Load the city data from `places.csv`.
* Start the tour at **Place 1**.
* Limit the tour to 50 cities (for faster execution).
* Use the **2-opt algorithm** to find the optimal route.
* Ensure that the tour returns to **Place 1** at the end.

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Contributing

Feel free to fork the repository, create issues, or submit pull requests to enhance the project. Contributions are welcome!

---

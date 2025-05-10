# Traveling Salesman City-Tour Optimizer

This project solves a variation of the **Traveling Salesman Problem (TSP)**, where the goal is to determine the most efficient route for visiting multiple cities and returning to the starting city. The project implements several algorithms to optimize the tour, including a **Greedy Algorithm**, **2-opt Algorithm**, and **Simulated Annealing**. It reads city data from a CSV file, calculates distances between cities using the **Haversine formula**, and provides an interactive solution through a command-line interface (CLI).

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

   The `requirements.txt` file includes the necessary Python libraries such as `argparse`, `math`, and `json`.

---

## Project Structure

* **tsp.py**: Main script that contains the logic to solve the TSP using different algorithms.
* **tsp\_solver.py**: Contains the specific TSP-solving algorithms (Greedy, 2-opt, Simulated Annealing).
* **places.csv**: Sample CSV file containing city names and their latitude and longitude coordinates.
* **route.geojson**: Output file containing the optimal route in GeoJSON format.

---

## How to Run

### Step 1: Prepare the CSV File

The cities and their coordinates should be stored in a CSV file (e.g., `places.csv`). The file should follow this structure:

| City Name    | Latitude | Longitude |
| ------------ | -------- | --------- |
| Eiffel Tower | 48.8584  | 2.2945    |
| Place 2      | 48.8647  | 2.2968    |
| Place 3      | 48.8629  | 2.2903    |
| ...          | ...      | ...       |

Ensure the CSV file is in the correct format and located in the same directory as `tsp.py`.

### Step 2: Run the Script

You can run the script from the command line with the following syntax:

```bash
python tsp.py --csv <CSV_FILE> --start "<START_LOCATION>" --<OTHER_OPTIONS>
```

### Command-Line Arguments

* **--csv**: Path to the CSV file containing city names and coordinates.
* **--start**: The city name from which the tour should begin.
* **--limit**: (Optional) Limits the number of cities for faster testing. Default is `None`.
* **--algo**: Algorithm to solve the TSP. Choose from:

  * `greedy`: Uses the Greedy algorithm (default).
  * `2opt`: Uses the 2-opt algorithm for optimization.
  * `simulated-annealing`: Uses the Simulated Annealing algorithm.
* **--should-return**: (Optional) If provided, the algorithm will make sure the tour returns to the starting city after visiting all cities.

### Example Command

To run the script with a 50-city limit and use the Greedy algorithm:

```bash
python tsp.py --csv places.csv --start "Place 1" --limit 50 --algo greedy --should-return
```

This command does the following:

* Loads the cities from `places.csv`.
* Starts the tour from **"Place 1"**.
* Limits the number of cities to 50.
* Uses the **Greedy algorithm** to find the shortest route.
* Returns to the starting city after the tour.

---

## Expected Output

After running the script, you will get the following outputs:

1. **Optimal Tour**: The cities in the optimal order (printed in the console).
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

Starts from a given city and iteratively picks the nearest unvisited city. This approach provides a solution quickly but does not guarantee the optimal result.

### 2. **2-opt Algorithm**

Improves upon the Greedy solution by swapping two edges if it shortens the total path. This method can provide better solutions than Greedy.

### 3. **Simulated Annealing**

A probabilistic algorithm that escapes local minima by allowing "bad" moves, which may later lead to better solutions. The algorithm uses a cooling schedule to gradually reduce the chance of accepting worse solutions.

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

### Contributing

Feel free to fork the repository, create issues, or submit pull requests to enhance the project. Contributions are welcome!

---

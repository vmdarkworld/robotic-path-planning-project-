# robotic-path-planning-project-
🤖 Dijkstra Path Planning A 2D robotic path planning project using Dijkstra's Algorithm. Finds the optimal, shortest, collision-free path on a grid map. Includes C-space obstacle handling and visualization.
Here is a professional, comprehensive GitHub README in **Markdown** format. It breaks down the complex project into easy-to-understand, step-by-step processes for clarity.

## 🤖 Robotic Path Planning: Dijkstra's Algorithm Integrated with SLAM

This project demonstrates a complete solution for **autonomous robot navigation** by integrating **Simultaneous Localization and Mapping (SLAM)** for environment modeling and **Dijkstra's Algorithm** for **optimal path planning**. The goal is to find the **shortest, collision-free path** for a robot on a generated map.

-----

## ✨ Core Features & Components

The system is split into two primary phases: Mapping and Pathfinding.

### 1\. 🗺️ Environment Mapping (SLAM)

  * [cite_start]**Function:** Generates an accurate map of an unknown environment while tracking the robot's pose (position and orientation)[cite: 528]. [cite_start]This is crucial in environments where GPS is unavailable[cite: 529].
  * [cite_start]**Techniques Used:** **Visual SLAM** (using camera data) [cite: 541][cite_start], specifically mentioning **ORB SLAM** and **LSD-SLAM**[cite: 526, 567].
  * **Map Output:** An **Occupancy Grid Map** where obstacles and free space are clearly defined .

### 2\. 🧭 Path Planning (Dijkstra's Algorithm)

  * [cite_start]**Function:** Finds the optimal route in the weighted graph created from the SLAM map[cite: 415, 479].
  * [cite_start]**Algorithm Choice:** **Dijkstra's Algorithm** was chosen because it is guaranteed to find the **absolute shortest path** in a weighted graph[cite: 481, 524].

-----

## 🛠️ Step-by-Step System Implementation

### Phase I: Map Generation (Visual SLAM Process)

The robot uses its camera to perform the following steps in real-time to build the map:

1.  [cite_start]**Data Collection:** Capture a continuous stream of images[cite: 546].
2.  [cite_start]**Feature Extraction:** Identify key points of interest (e.g., corners or edges) from the images[cite: 547].
3.  [cite_start]**Pose Estimation:** Match features between consecutive images to estimate the camera's motion in 3D space, determining its position and orientation (pose)[cite: 552, 553].
4.  [cite_start]**Map Construction:** Continuously update the map, typically as a **sparse or semi-dense 3D structure** (e.g., using LSD-SLAM)[cite: 554, 579].
5.  [cite_start]**Optimization:** Refine the estimated poses and map using techniques like bundle adjustment to ensure accuracy[cite: 555].

### Phase II: Path Calculation (Dijkstra's Algorithm)

Once the environment is mapped, Dijkstra's algorithm executes on the resulting grid (treated as a weighted graph):

1.  [cite_start]**Initialization:** Assign a distance of **'0'** to the **source vertex** (start node) and **'inf'** (infinity) to all other vertices[cite: 488, 489].
2.  [cite_start]**Shortest Set Creation:** Maintain a set of vertices for which the shortest path has been finalized (shortest path tree set)[cite: 485].
3.  [cite_start]**Vertex Selection:** **Pick the unvisited vertex 'u'** that has the **minimum distance value** recorded so far[cite: 490].
4.  **Relaxation:** For each neighbor 'v' of 'u', check if the new path through 'u' is shorter than the currently recorded distance to 'v'. [cite_start]If so, update $d(v)$[cite: 491].
    $$\text{If } d(u) + c(u, v) < d(v) \text{, update } d(v)$$
5.  **Iteration:** Repeat steps 3 and 4 until all vertices have been processed or the goal is reached .
6.  **Path Reconstruction:** Trace back from the goal to the start using the stored predecessor pointers to find the **optimal shortest path**.

-----

## 🔬 Algorithm Analysis & Comparison

| Feature | [cite_start]BFS (Breadth-First Search) [cite: 523] | [cite_start]$A^{*}$ Algorithm [cite: 523] | [cite_start]Dijkstra's Algorithm [cite: 523] |
| :--- | :--- | :--- | :--- |
| **Type** | Uninformed Search | **Informed Search** | Uninformed Search |
| **Goal** | [cite_start]Shortest path (fewest edges) in **unweighted** graphs [cite: 523] | [cite_start]Shortest path **with heuristic** [cite: 523] | [cite_start]Find the **shortest path in weighted graphs** [cite: 523] |
| **Heuristic** | [cite_start]None [cite: 523] | [cite_start]Uses $h(n)$ [cite: 523] | [cite_start]**None** [cite: 523] |
| **Complexity** | [cite_start]$O(V+E)$ [cite: 523] | [cite_start]$O((V+E)\log V)$ [cite: 523] | [cite_start]**$O((V+E)\log V)$** [cite: 523] |

[cite_start]**Why Dijkstra's?** It was chosen because it **guarantees the shortest path** in a weighted graph, even though its computational complexity is similar to $A^{*}$[cite: 524]. $A^{*}$'s performance relies heavily on having a good heuristic.

-----

## 💡 Project Results

  * [cite_start]**Result:** The system successfully identified the shortest path for the robot on the SLAM-generated map[cite: 526].
  * **Path Distance:** The computed shortest distance between the start and goal was **43.83 grid units**.

-----

## 🤝 Getting Started (Local Setup)

1.  **Clone the Repository:**
    ```bash
    git clone [repository-link]
    cd path-planning-project
    ```
2.  **Prerequisites:** (List necessary Python libraries, etc.)
    ```bash
    # Example dependencies (adjust as needed for your code)
    pip install numpy matplotlib opencv
    ```
3.  **Run Simulation:**
    ```bash
    python main_dijkstra.py
    ```

## ⏭️ Future Work

  * Compare the performance of Dijkstra's algorithm with the $A^{*}$ algorithm.
  * [cite_start]Extend the system to handle **dynamic obstacles** (moving objects), a known challenge for these static path planners[cite: 335, 477, 408].
  * [cite_start]Mitigate issues like **getting stuck in dead ends** or **infinite loops in cyclic graphs** (disadvantages noted for related graph search methods like DFS)[cite: 405, 409].

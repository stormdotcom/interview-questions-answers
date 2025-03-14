
# QuadTree and Nearest Neighbors

## QuadTree

A **QuadTree** is a spatial data structure used for **efficient partitioning of a 2D space**. It is widely used in **geographic information systems (GIS), nearest neighbor searches, and image processing**.

### 1. QuadTree Creation

- The **entire map (dataset)** is treated as a **root node**.
- If a node contains **more than X (e.g., 100) points**, it is **subdivided into four quadrants**.
- The process continues **recursively** until each **leaf node** contains at most **X points**.

#### **Steps to Create a QuadTree**

1. **Step 1:** Start with the **root node** containing all locations.
2. **Step 2:** If the node has **>100 points**, it is **split into four equal quadrants**.
3. **Step 3:** Recursively check each quadrant. If a quadrant has **>100 points**, **subdivide it further**.
4. **Step 4:** Continue until **each leaf node contains ≤100 points**.

---

### 2. Finding the Grid ID (Finding a Point’s QuadTree Node)

To determine which grid a point `(x, y)` belongs to:

1. Compare `x` and `y` with the **midpoint** of the current node’s bounding box.
2. Determine which **quadrant** the point falls into.
3. Recursively navigate **down the tree** until a **leaf node** is found.
4. The **leaf node ID** is the **Grid ID**.

---

### 3. Adding a New Place

- **Find the grid ID** for `(x, y)`.
- Add the place to the **corresponding leaf node**.
- If the **leaf node exceeds 100 points**, **split it into four smaller nodes**.
- Redistribute the points among the four new children.

---

### 4. Deleting a Place

- Find the **grid ID** of the point.
- Remove it from the **leaf node**.
- If the **combined count of four children falls below 100**, **merge them into a single parent node**.

---

### 5. Storing a QuadTree

Each node stores:

- **Top-left and bottom-right coordinates** (16 bytes each).
- **Four pointers** to child nodes (4 bytes each).

#### **Storage Calculation**

- **100 million places** → **100 million leaf nodes**.
- **Total nodes (including internal nodes) ≈ 6.5 million**.
- **Total storage required ≈ 4GB**.
- **Fits easily in RAM (e.g., 64GB systems)**.

---

## Nearest Neighbor Search

**Nearest Neighbor (NN) Search** is used in **location-based services**, such as **Google Maps, Uber, and GIS applications**.

### 1. Brute Force Approach

- Compute **Euclidean distance** for every location `(x1, y1)`, `(x2, y2)`:
  \[
  d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}
  \]
- Sort the results and return the **top K nearest locations**.
- **Issue:** Slow for large datasets.

---

### 2. Finding Locations Inside a Square

- Instead of searching the whole world, **search within a bounding square** around `(x, y)`.
- SQL Query:
  ```sql
  SELECT * FROM places
  WHERE lat < x + k AND lat > x - k
  AND long < y + k AND long > y - k;
  ```


- **Issues:**
  - Choosing the right **`k`** (bounding distance) is difficult.
  - **Slow queries** when dealing with millions of points.

---

### 3. Grid-Based Approach

- **Divide the world into grids** (e.g., `1km × 1km` cells).
- Store locations **inside grid cells**.
- Query **your grid + adjacent grids** for nearby points.

#### **Problem:** Fixed grid sizes don't work well for cities vs oceans.

#### **Solution:** Use **variable-size grids** based on location density.

---

### 4. Using QuadTree for Nearest Neighbors

- **Find the Grid ID** for the query `(x, y)`.
- Retrieve **all locations in that grid**.
- If not enough results, query **neighboring grids**.
- Methods to find neighbors:
  - **Sibling pointers** (track adjacent grids).
  - **Probing nearby points** to get their grid IDs.

---

### 5. Dynamic Systems (e.g., Uber)

- **Taxis move**, making location tracking complex.
- Solution:
  - **Use a real-time QuadTree update mechanism**.
  - **Efficiently track moving objects** with **low-latency updates**.

---

## **Summary**

- **QuadTree efficiently organizes spatial data** into **variable-sized grids**.
- **Nearest neighbor search can be done using QuadTree, grids, or brute force**.
- **QuadTree improves search speed significantly** compared to brute-force methods.
- **It fits within RAM and is scalable** (100M locations in ~4GB).
- **Used in location-based services like Google Maps, Uber, and GIS applications**.

---

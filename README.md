# curvetopia_final
https://youtu.be/WFHyMASlDE8?si=-wFU8Q3jeGmA_7UZ
## Overview

This script is designed to load, process, and visualize polyline data from a CSV file. It begins by reading the polylines, representing various paths, and then processes them through a series of transformations to simplify and classify the paths into geometric shapes. The script ultimately provides a visual comparison between the original and processed data, highlighting differences and emphasizing the importance of symmetry in geometric analysis.

## Features

- **Polyline Loading**: Load polyline data from a CSV file, where each path is represented by a unique combination of `path_id` and `segment_id`.
- **Path Simplification**: Reduce the polylines into straight-line segments, making them easier to work with computationally.
- **Path Splitting**: Detect and split paths at sharp turns, facilitating better processing.
- **Path Merging**: Combine adjacent polylines into longer, coherent paths, followed by further simplification into straight lines.
- **Shape Classification**: Classify processed paths into geometric shapes such as circles, ellipses, and rectangles.
- **Symmetry Analysis**: Add symmetry lines to shapes like circles and rectangles in the visualization to emphasize symmetry and detect any deviations.
- **Visual Comparison**: Display a side-by-side comparison of the original and processed polylines, highlighting the transformations made.

## Usage

### Prerequisites

Ensure that you have Python installed along with the following libraries:
- `numpy`
- `matplotlib`

You can install these libraries using pip:
```bash
pip install numpy matplotlib
```

### Script Execution

1. **Prepare the CSV File**: Place the CSV file containing the polyline data in the specified directory (`./examples/occlusion2.csv` by default). Ensure the file is formatted correctly, with each line representing a path segment.

2. **Run the Script**: Execute the script in your Python environment.

3. **Visual Output**: After execution, the script will generate a figure with two side-by-side plots:
   - The **left plot** shows the original polylines.
   - The **right plot** shows the processed polylines, including any symmetry lines added during geometric shape classification.

4. **Shape Count Analysis**: The script will also output the count of each detected shape (e.g., circles, rectangles) for further analysis.

### Example Code

```python
csv_path = "./examples/occlusion2.csv"

output_data1 = read_csv_(csv_path)
output_data2 = read_csv_(csv_path)
output_data2 = process_paths(output_data2)

fig, axs = plt.subplots(1, 2, tight_layout=True, figsize=(16, 8))
plot(output_data1, 'Original Data', axs[0])
plot(output_data2, 'Processed Data', axs[1])
plt.show()
```

### Explanation

- **Original Data (`output_data1`)**: Kept unchanged for later comparison.
- **Processed Data (`output_data2`)**: Undergoes a series of transformations:
  - **Splitting at Sharp Turns**: Breaks paths at sharp angles to ease processing.
  - **Simplification**: Reduces polylines to straight-line segments.
  - **Merging**: Combines adjacent polylines into longer paths.
  - **Classification**: Categorizes paths into geometric shapes and counts them.
  - **Symmetry Lines**: Adds symmetry lines to shapes like circles and rectangles to visualize and analyze symmetry.

### Visualization

The visualization serves two purposes:
1. **Comparison**: Observe the difference between the original and processed data.
2. **Symmetry Emphasis**: The symmetry lines in the second plot help in identifying any deviations from perfect symmetry, crucial for applications where precision in shape recognition is important.

## Conclusion

This script provides a comprehensive solution for processing and visualizing polyline data, particularly useful in applications requiring path simplification, shape classification, and symmetry analysis. By comparing the original and processed paths, users can gain insights into how the data was transformed and how well it conforms to ideal geometric shapes.

# occlusion_partial

## Overview

This code is designed to process and visualize path data, focusing on detecting and handling overlaps between paths. It includes functionality for visualizing paths, identifying overlaps, and simplifying paths based on detected overlaps and angles. The final output provides a comparison between the original and processed paths.

## Functions

1. **`plot(paths_XYs, title, ax)`**
   - **Description:** Visualizes paths on a graph. Different colors are used to distinguish between paths.
   - **Parameters:**
     - `paths_XYs` (list of np.ndarray): List of arrays with XY coordinates of paths.
     - `title` (str): Title for the plot.
     - `ax` (matplotlib.axes.Axes): Matplotlib axis object for plotting.

2. **`find_overlap(path1, path2, atol=0.1)`**
   - **Description:** Identifies overlapping segments between two circular paths by comparing the proximity of points.
   - **Parameters:**
     - `path1` (np.ndarray): Array of XY coordinates for the first path.
     - `path2` (np.ndarray): Array of XY coordinates for the second path.
     - `atol` (float): Absolute tolerance for point proximity (default is 0.1).
   - **Returns:** List of tuples representing start and end indices of overlapping segments in both paths.

3. **`are_almost_parallel(vector1, vector2, tolerance=0.1)`**
   - **Description:** Checks if two vectors are nearly parallel by comparing their dot product within a specified tolerance.
   - **Parameters:**
     - `vector1` (np.ndarray): First vector.
     - `vector2` (np.ndarray): Second vector.
     - `tolerance` (float): Tolerance for determining parallelism (default is 0.1).
   - **Returns:** Boolean indicating if the vectors are almost parallel.

4. **`is_sharp_angle(path, index)`**
   - **Description:** Determines if the angle at a specific point in a path is sharp.
   - **Parameters:**
     - `path` (np.ndarray): Array of XY coordinates representing the path.
     - `index` (int): Index of the point where the angle is being checked.
   - **Returns:** Boolean indicating if the angle is sharp.

5. **`remove_overlap_with_straight_line(path, overlap_start, overlap_end)`**
   - **Description:** Removes overlapping segments from a path and replaces them with a straight line.
   - **Parameters:**
     - `path` (np.ndarray): Array of XY coordinates representing the path.
     - `overlap_start` (int): Starting index of the overlap.
     - `overlap_end` (int): Ending index of the overlap.
   - **Returns:** Modified path with overlap removed and replaced by a straight line.

6. **`process_paths(paths_XYs, angle_threshold=130)`**
   - **Description:** Processes paths by removing overlapping portions with sharp angles and replacing them with straight lines.
   - **Parameters:**
     - `paths_XYs` (list of np.ndarray): List of arrays with XY coordinates of paths.
     - `angle_threshold` (int): Angle threshold to determine sharp angles (default is 130 degrees).
   - **Returns:** List of processed paths.

## Usage

1. **Load Data:**
   - Load polyline data from a CSV file into two variables using the `read_csv_` function.

2. **Initial Processing:**
   - Split paths at sharp turns, simplify them into straight-line segments, and merge adjacent polylines.

3. **Refinement:**
   - Further simplify and merge collinear segments.

4. **Classification:**
   - Classify processed paths into geometric shapes and count each shape.

5. **Visualization:**
   - Create a side-by-side plot to compare original and processed paths.

## Example

```python
csv_path = "./examples/occlusion2.csv"

# Load data
output_data1 = read_csv_(csv_path)
output_data2 = read_csv_(csv_path)

# Process paths
output_data2 = process_paths(output_data2)

# Plot and compare
fig, axs = plt.subplots(1, 2, tight_layout=True, figsize=(16, 8))
plot(output_data1, 'Original Data', axs[0])
plot(output_data2, 'Processed Data', axs[1])
plt.show()
```

## Dependencies

- `numpy`
- `matplotlib`


# curvetopia_final

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

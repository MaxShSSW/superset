# Waterfall Chart Sorting Modification

## Overview
This modification adds sorting functionality to the Apache Superset waterfall chart, allowing users to sort the chart by metric values in addition to the existing category-based sorting.

## Changes Made

### 1. Control Panel (`controlPanel.tsx`)
- Added a new "Sort by Values" control with the following options:
  - `none`: No sorting (default behavior)
  - `ascending`: Sort by ascending values
  - `descending`: Sort by descending values
  - `absolute_ascending`: Sort by absolute values in ascending order
  - `absolute_descending`: Sort by absolute values in descending order

### 2. Types (`types.ts`)
- Added `WaterfallSortByValues` type definition
- Updated `EchartsWaterfallFormData` to include `sortByValues` field
- Updated `DEFAULT_FORM_DATA` to include default sorting value

### 3. Transform Logic (`transformProps.ts`)
- Added `sortData` function to handle different sorting algorithms
- Modified `transformer` function to accept and use sorting parameter
- Updated the main `transformProps` function to pass sorting configuration
- Implemented sorting logic that preserves the waterfall chart structure while reordering data points

## Sorting Options

1. **None**: Maintains original data order
2. **Ascending**: Sorts from smallest to largest values
3. **Descending**: Sorts from largest to smallest values
4. **Absolute Ascending**: Sorts by absolute values from smallest to largest
5. **Absolute Descending**: Sorts by absolute values from largest to smallest

## Implementation Details

The sorting is applied after the initial data transformation but before the final waterfall chart series generation. The implementation:

- Preserves the total row at the end of the chart
- Maintains the breakdown structure when breakdowns are used
- Handles both positive and negative values correctly
- Works with the existing waterfall chart logic

## Testing

Added unit tests to verify:
- Sorting functionality works correctly
- Existing functionality remains intact
- Different sorting options produce expected results

## Usage

Users can now select the "Sort by Values" option in the chart control panel to sort their waterfall chart by metric values instead of being limited to category-based sorting only.

## Files Modified

1. `superset-frontend/plugins/plugin-chart-echarts/src/Waterfall/controlPanel.tsx`
2. `superset-frontend/plugins/plugin-chart-echarts/src/Waterfall/types.ts`
3. `superset-frontend/plugins/plugin-chart-echarts/src/Waterfall/transformProps.ts`
4. `superset-frontend/plugins/plugin-chart-echarts/test/Waterfall/transformProps.test.ts`
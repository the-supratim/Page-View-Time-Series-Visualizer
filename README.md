# Page View Time Series Visualizer

This is the boilerplate for the Page View Time Series Visualizer project. Instructions for building your project can be found at https://www.freecodecamp.org/learn/data-analysis-with-python/data-analysis-with-python-projects/page-view-time-series-visualizer

### Project Description: Page View Time Series Visualizer

The Page View Time Series Visualizer project involves creating a function to visualize the page view statistics over time from a dataset. You will analyze and visualize the data to identify trends, peaks, and anomalies in the page view traffic.

### Objectives

1. **Read and Process the Dataset**: Load the dataset from a CSV file and process the date and page view information.
2. **Visualize the Data**: Generate a line plot of the page views over time, with additional enhancements like rolling averages and anomalies.
3. **Return the Visualization**: Display or save the plot in a specified format.

### Dataset

The dataset contains the following columns:
- `date`: The date of the page view (formatted as `YYYY-MM-DD`).
- `value`: The number of page views on that date.

### Function Specifications

1. **Input**: Path to the CSV file.
2. **Output**: A plot showing the time series of page views with:
   - A line graph of page views over time.
   - A rolling average line to highlight trends.
   - Annotations for any anomalies or significant peaks.

### Steps to Follow

1. **Load the Data**:
   - Use pandas to read the CSV file into a DataFrame.
   - Ensure that the `date` column is parsed as a datetime object.

2. **Process the Data**:
   - Set the `date` column as the DataFrame index.
   - Sort the DataFrame by the `date` column to ensure chronological order.

3. **Visualize the Data**:
   - Use Matplotlib or Seaborn to create a line plot of the page views over time.
   - Add a rolling average line to smooth out short-term fluctuations and highlight longer-term trends.
   - Use anomaly detection or highlight significant peaks.

4. **Enhance the Plot**:
   - Add labels, titles, and grid lines for better readability.
   - Optionally, annotate the plot with significant events or anomalies.

5. **Save or Display the Plot**:
   - Save the plot to a file or display it in an interactive window.

### Example Implementation

Here's a detailed implementation using `matplotlib` and `pandas`:

```python
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib.dates import DateFormatter
from statsmodels.tsa.seasonal import seasonal_decompose

def draw_line_plot(file_path):
    # Load data
    df = pd.read_csv(file_path)
    df['date'] = pd.to_datetime(df['date'])
    df.set_index('date', inplace=True)
    df.sort_index(inplace=True)

    # Create figure and axis
    fig, ax = plt.subplots(figsize=(14, 7))

    # Plot the data
    ax.plot(df.index, df['value'], label='Page Views', color='blue')
    
    # Adding rolling average line
    df['rolling_avg'] = df['value'].rolling(window=7).mean()
    ax.plot(df.index, df['rolling_avg'], label='7-Day Rolling Average', color='red')

    # Formatting the plot
    ax.set_title('Daily Page Views', fontsize=16)
    ax.set_xlabel('Date', fontsize=12)
    ax.set_ylabel('Page Views', fontsize=12)
    ax.legend()
    ax.grid(True)
    ax.xaxis.set_major_formatter(DateFormatter('%Y-%m-%d'))
    
    # Rotate date labels
    plt.xticks(rotation=45)
    
    # Display the plot
    plt.tight_layout()
    plt.show()

def draw_bar_plot(file_path):
    # Load data
    df = pd.read_csv(file_path)
    df['date'] = pd.to_datetime(df['date'])
    df.set_index('date', inplace=True)
    df.sort_index(inplace=True)
    
    # Resample data to get monthly averages
    df_monthly = df.resample('M').mean()
    
    # Create figure and axis
    fig, ax = plt.subplots(figsize=(14, 7))
    
    # Plot the data
    df_monthly['value'].plot(kind='bar', ax=ax, color='skyblue')
    
    # Formatting the plot
    ax.set_title('Monthly Average Page Views', fontsize=16)
    ax.set_xlabel('Month', fontsize=12)
    ax.set_ylabel('Average Page Views', fontsize=12)
    
    # Display the plot
    plt.tight_layout()
    plt.show()

def draw_box_plot(file_path):
    # Load data
    df = pd.read_csv(file_path)
    df['date'] = pd.to_datetime(df['date'])
    df.set_index('date', inplace=True)
    df.sort_index(inplace=True)
    
    # Create figure and axis
    fig, ax = plt.subplots(figsize=(14, 7))
    
    # Plot the data
    df['value'].plot(kind='box', vert=False, ax=ax)
    
    # Formatting the plot
    ax.set_title('Box Plot of Page Views', fontsize=16)
    ax.set_xlabel('Page Views', fontsize=12)
    
    # Display the plot
    plt.tight_layout()
    plt.show()

def draw_all_plots(file_path):
    draw_line_plot(file_path)
    draw_bar_plot(file_path)
    draw_box_plot(file_path)

# Example usage
file_path = 'page_views.csv'
draw_all_plots(file_path)
```

### Expected Output

1. **Line Plot**: A line graph showing page views over time with a 7-day rolling average.
2. **Bar Plot**: A bar chart showing the monthly average page views.
3. **Box Plot**: A box plot depicting the distribution of page views.

This project helps you practice data visualization using Python libraries like Matplotlib and Seaborn, and it also enhances your skills in handling and processing time series data.

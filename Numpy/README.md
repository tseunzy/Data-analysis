
# NumPy (Python) – Learning Notes + Practice (USED JUPYTER FOR THIS PROJECT)

    This folder contains my hands-on learning notes and practice scripts for **NumPy**, the core Python library for fast numerical computing. I used NumPy to work with arrays, do vectorized math (no loops), clean data, reshape matrices, and perform basic linear algebra.


    Arrays and Shapes
    - Creating 1D and 2D arrays with np.array, np.arange, np.linspace
    - Understanding shape, dtype

    Indexing, Slicing, and Masking
    - Selecting values using indices and slices:
    - Boolean masking for filtering and cleaning: a[a > 6], m[m < 4] = 0

    Vectorized Operations and Broadcasting
    - Doing math on arrays without loops
    - Broadcasting with different shapes

    Aggregations and Statistics
    - Summaries across rows/columns using --axis, sum, mean, min, max, std
    - Working with cumulative and change operations

    Data Cleaning Utilities
    - Replacing values based on conditions: np.where(), np.clip() to clamp values into a range
    - Handling missing values with 'NaN': np.nanmean() to compute mean ignoring missing values
    - filling missing values with 'np.where(np.isnan(a), mean, a)'

    Saving and Loading Data
    - Saving/loading NumPy binary files: np.save() and np.load()
    - Saving/loading CSV files: np.savetxt() and np.loadtxt(), 
    - genfromtxt() load everything as dtype=str so it doesn’t crash
    - delimiter=',',dtype=, missing_values=, filling_values=,usecols=(load only needed columns),skip_header=.

    Linear Algebra Basics
    - Matrix multiplication: A @ B (preferred) and np.dot(A, B)

    Mini Examples


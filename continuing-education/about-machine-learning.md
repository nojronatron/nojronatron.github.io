# Machine Learning

Introduction to Machine Learning

## About AI and ML

Artificial Intelligence (AI): Science of getting machines to accomplish tasks that typically require human level experience and skills.

Machine Learning (ML): A subset of AI

Deep Learning: A further class of AI and ML, beyond the scope of this writup.

## Classical Machine Learning

Why use it?

- Calculate likelihood of upcoming events or medical conditions.
- Anticipate weather events.
- Understand sentiments of a writing.
- Detect propaganda or untrue statements and informational.

### ML Core Concepts

### ML History

- Started in 1950's.
- Alan Turing: Develop a machine that can "think". Turing Test can help determine difference between human and non-human responses to inputs.
- Golden Years: 1956 to 1974 :arrow_right: Optimism was high and government funding helped develop AI.
- One development was Eliza: Early text-based chat-bot / therapist.
- AI Winter in 1980's: Funding dried up, and personal computers competed with large AI-targeted systems.
- Rise of Internet and Smart Phones helped make large data-set processing possible.
- Big Data: Data set sizes that are very large and processing of such became capable in the 2000's.

### ML Statistical Techniques

Includes: Regression, Classifications, Clustering, etc.

Core concepts:

- Is AI the correct approach to solve the problem?
- Data must be collected and prepared
- Models must be trained
- Model performance and functionality must be evaluated
- Hyperparameters must be tuned
- Real-world testing of trained model is necessary

Additional tidbits:

- A _lot_ of information freely available online that can be used.
- When plenty of input data is available related to the problem, AI could be a good approach.
- Data normalization is probably necessary before using it.
- Data should be split into training (80%) and for testing (20%).
- Model training algorithms vary, so evaluate algorithms for one that will fit the problem domain.

### Tools To Build and Use ML

- IDE: GH CodeSpaces, VSCode, etc.
- Language: Python is a good choice.
- Jupyter Notebooks: Text, Code, and Visualization tool.
- VSCode Extension: Python Extension.
- Git.

Note: Windows Store can be used to install Python3.

### Regression Models

Investigate the relationship between variables.

- Plot x,y data and use regression to find the general trend of the data.
- Enables predicting y, given x.

Linear Regression: Straight-line trend between data points. Useful for numerical data analysis.

Polynomian Regression: Curved regression plotting e.g. x^2 + 2x + 3

Logistic Regression: Categorical prediction based on results nearing 0 or 1.

### Build Regression Models

1. Install Python 3 and Jupyter Notebooks (see [Jupyter Notebooks](https://jupyter.org/) for more).
2. Clone `ML-for-beginners.git` from GitHub.
3. Activate venv and add `.venv` to GitIgnore.
4. Pip Install Pandas - Data analysis and manipulation tool.
5. Pip Install MatPlotLib - Create data visualizations.
6. Pip Install NumPy - Library used in scientific computing.
7. Pip Install SciKit-Learn - Predictive data analysis.
8. Pip Install IPyKernel - backend for Jupyter Notebooks.

Note: Use `venv` to virtualize environments (.venv directory within the project).

Note: Use `piplist` or browse the 'lib' directory to verify installations succeeded.

### Analyze and Clean Data

Note: Empty cells within data will not be helpful before extracting information from it.

A DataFrame is a subset of data that has been normalized and prepared for use in ML.

1. Determine which columns of data are actually necessary for the current analysis.
2. Filter-out rows with empty cells data.
3. Drop columns that are not necessary for this analysis.
4. Normalize the data implementing code that compares data types in equivalent amounts. E.g. bushel sizes, or quarts vs gallons.

Key Takeaway: Python code will need to be written to cleans data, so become familiar with traversing data, finding non-normalized data cells, and applying a function to normalize them while creating a Data Frame.

### Using MatPlotLib

MatPlotLib:

- Create data visualizations.
- Utilizes Python.

Data visualiation types: Plot, Scatter, Bar, Vector Fields, Statistics, Contours, and more.

Graph visualizations can be adjusted using many built-in options.

Note: Pandas uses MatPlotLib.

## Resources and Attributions

Primary source of material is from Microsoft Reactor: [Introduction to Machine Learning for Beginners](https://www.youtube.com/playlist?list=PLlrxD0HtieHjNnGcZ1TWzPjKYWgfXSiWG).

Host: Beatriz Stollnitz @beastollnitz - Principal Cloud Advocate AI/ML.

## Footer

Return to [ContEd Index](./conted-index.html)

Return to [root README](../README.html)

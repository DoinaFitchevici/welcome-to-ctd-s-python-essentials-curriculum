# Lesson 05 — Data Wrangling and Aggregation

## Overview

No overview provided

## Learning Objectives

- Students will learn to manipulate, summarize, and combine datasets in Pandas using selection, aggregation, merging, and transformation methods. They will practice accessing specific data, performing group-level calculations, and combining data from multiple sources.

## Topics Covered

- 1. Pandas Review (Optional): Recap of Series, DataFrames, and key methods from Lesson 3.
- 2. Data Selection: Selecting subsets with `.loc[]`, `.iloc[]`, `.at[]`, and `.iat[]`; filtering rows by conditions; applying string methods.
- 3. Data Aggregation: Grouping data with `groupby()`; applying functions like `sum()`, `mean()`, and `count()`; using `agg()` for multiple aggregations.
- 4. Merging and Joining: Combining DataFrames with `merge()` and `join()`; inner, outer, left, and right joins; joining on one or multiple keys.
- 5. Data Transformation: Adding, updating, and deleting columns; using operators, Series methods, `map()`, and NumPy functions for transformation.
- 6. Utility Methods: Renaming columns, setting or resetting index, and sorting data.

## Status

pending

## Assignment

Assignment for Lesson 5

### Objective

No objective specified

### Expected Capabilities

Expected capabilities will be defined as the lesson progresses.

### Instructions

Instructions will be provided when the lesson is generated.

### Tasks

#### Task 1: Task 1

## Lesson 5 Assignment — Data Wrangling and Manipulation
### Advanced Data Wrangling and Aggregation with Pandas

### **Objective:**
The purpose of this assignment is to deepen your understanding of data wrangling and aggregation using the Pandas library in Python. You will work with sample DataFrames to perform various operations such as filtering, handling missing values, merging, sorting, and transforming.

### **Setup**

The assignments up to this one have required you to create `.py` files and to submit them by creating pull requests for your python_homework repository.  For this assignment, you create a Jupyter notebook file.  Jupyter notebooks are a way to do data presentation and analysis, using Python code.  A notebook is comprised of a sequence of cells, which come in two kinds: Markdown cells, for putting in the text you want to show, and code cells, where you put your Python code.

With a little setup, you can create Jupyter notebooks in VSCode, and submit them to GitHub.  However, GitHub is not a friendly environment for collaboration on notebooks.  Your reviewer wants to see the notebooks, to run them, and to give you comments in context.  For that purpose, we use [https://kaggle.com].  That site also has an interesting collection of data sets you can use for practice in data analysis and presentation.  Connect to the site now and register, so that you have an account.

### **Tasks:**

### **Task 1: Data Selection**
1. **On the Kaggle site, click on the plus button in the upper left, and create a notebook called CTD_Assignment_5.**  It comes up with a code cell already present.  Leave that one alone, and click on the plus markdown button to add a cell that says "Task 1". You do not have to use markdown formatting directives, however if you do choose to use formatting, it's worth noting that level two headings starting with '## ' are automatically added to the table of contents.  This is how you convey information about your code to your reviewer, Jupyter notebook style.  After adding a markdown cell, click on the plus code button to add another cell.  You add the code for this task to the cell.  As you complete each of the following tasks, run the cell to make sure your code works.  You run the cell by clicking on the arrow at the top left of the cell.

**Note:** The various code cells in a Jupyter notebook are all part of the same program, so you have access to the variables and functions of one cell from each of the ones that follow.  You only need to import Pandas once, for example.  However, Kaggle sessions **time out** if you go to the kitchen for a sandwich or something.  When they time out, your variables go away.  So, if you then run cell 2, which is dependent on something in cell 1, you'll get an error.  To correct this, click on the Run All button at the top of your Kaggle notebook screen, and the entirety of the program runs in the order the cells appear.

2. **Create DataFrames `df1`, `df2`, and `df3` using the provided sample data(feel free to change the values):**
   - `df1` contains names, ages, and salaries of five employees.
   - `df2` contains names, ages, and salaries of five other employees.
   - Display each DataFrame.
   
```
data1 = {
    'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eva'],
    'Age': [25, 30, 35, 40, 30],
    'Salary': [50000, 60000, 70000, 80000, 55000]
}
```

```
data2 = {
    'Name': ['Frank', 'Grace', 'Helen', 'Ian', 'Jack'],
    'Age': [28, 33, 35, 29, 40],
    'Salary': [52000, 58000, 72000, 61000, 85000]
}

data3 = {
    'Name': ['Frank', 'Helen', 'Ian', 'Hima', 'Chaka'],
    'Age': [17, 93, 12, 57, 106],
    'Favorite Color': ['blue', 'pink', 'burgundy', 'red', 'turquoise']
}
```
Print the resulting dataframes. 

3. **Perform the following selection operations on `df1`:**
   - Select the 'Name' column, and print the result.
   - Select both 'Name' and 'Salary' columns, and print the result.
   - Slice the first three rows using integer-based indexing (`iloc`), and print the result.

### **Task 2: Data Aggregation**

Again, you create a markdown cell to describe this task, and a code cell containing the code for the task.  Do this throughout, whenever you are doing your homework in Jupyter notebooks.

1. **Group `df1` by 'Age' and aggregate the 'Salary' column:**
   - Calculate the mean, sum, and count of the salary for each age group.
   - Display the aggregated results.

### **Task 3: Merging and Joining DataFrames**
1. **Merge `df1` and `df3` into `df_1_3_merged` on the 'Name' column:**
   - Use an outer merge to combine the two DataFrames and handle any missing data.
   - Use the suffixes `_left` and `_right` to differentiate columns from each DataFrame. (You specify `suffixes=['_left','_right']` on the call to merge.)
   - Display the result with print(). When you do, you will see some annoying warning messages that contain words like "Runtime Warning: invalid value encountered ...".  This is because of the NaN values in the frame.  You could suppress these warnings by 
      ```python
      np.warnings.filterwarnings('ignore')
      ```
      But, don't do this yet.  You might see some other warnings if you make a mistake, and you don't want to miss them.  Just ignore these particular warnings.
   - We see that the 'Salary' column has `NaN` values.  Transform this column to replace `NaN` with the starting salary of 15000.  Hint: fillna() can be used on a Series.
   - Also, transform the 'Favorite Color' column to replace `NaN` values with 'yellow'.
   - Display the result.
   - We have `NaN` for some of the entries in the 'Age_left' column.  For other rows, the `NaN` value is in the 'Age_right' column.  We want to create a new `Age` column, using the values from 'Age_left' if they are not `NaN`, and from 'Age_right' otherwise.  We'll use np.where().  As this is a new technique, the answer is as follows:
       ```python
       df_1_3_merged['Age'] = np.where(df_1_3_merged['Age_left'].notna(),df_1_3_merged['Age_left'], df_1_3_merged['Age_right'])
       # This works like a ternary expression.  If the expression passed to np.where is True, you get the left value, otherwise the right value.
       ```
   - Display the result.
   - Drop the 'Age_left' and 'Age_right' columns and display the result.

2. **Use the Join Method:**
   - Create new DataFrames df1_b and df3_b from df1 and df3.  In these new DataFrames, set 'Name' as the index.
   - Join the DataFrames with outer join logic and display the result.  Do not use `inplace=True`.  Unlike the merge method, the join method does not provide default suffixes if there are overlapping columns.  Check the online documentation to find out how to specify them.

### **Task 4: Filtering Rows Based on Conditions**
1. **Filter rows in `df1` where 'Age' is greater than 30:**
   - Display the filtered rows.

### **Task 5: Sorting Data**
1. **Sort `df1` by the 'Salary' column in descending order:**
   - Display the sorted DataFrame.

### **Task 6: Renaming Columns**
1. **Rename columns in `df1`:**
   - Rename 'Age' to 'Employee Age' and 'Salary' to 'Employee Salary'.  Do not use `inplace=True`, because then you wouldn't be able to do Task 9.
   - Display the DataFrame with the renamed columns.

### **Task 7: Data Transformation**
1. **Apply a transformation to the 'Salary' column in `df1`:**
   - Increase the salary by 10% for each employee.
   - Display the updated DataFrame.

### **Task 8: Concatenating DataFrames**
1. **Concatenate `df1` and `df2` to add the rows of `df2` to the end of `df1`**
   - Use `ignore_index=True` to reset the index.
   - Display the result.

### **Task 9: Data Wrangling a Kaggle Dataset**

Kaggle has some nice datasets you can use in exercises.  These are `csv` files.  We are going to do some data wrangling on one of those provided files. For this task, we are going to find the international football teams that are especially bad on defense.
- On the upper right of your notebook, click on 'Add Input'.  Click on the 'Datasets' button.  Then do a search on 'international football results'.  You should see one from Mart Jürisoo.  Click on the plus sign next to that one.  That adds the dataset to your notebook, so that you can read the CSV files.
- Create a markdown cell for Task 9, and then create a new code cell for the following steps.
- You need to find the available CSV file path names.  The first cell in your notebook, the one it started out with, has the following code:
    ```python
    import pandas as pd
    import os
    for dirname, _, filenames in os.walk('/kaggle/input'):
        for filename in filenames:
            print(os.path.join(dirname, filename))
    ```
   Click on this cell to make it active, and run the cell.  This will list, among others, the path `/kaggle/input/international-football-results-from-1872-to-2017/results.csv`.  This is the one you want.  Read it into a DataFrame called football_results.

- Print the first 5 lines of this file.
- All the entries have a home team and an away team.  This is kind of clumsy for us, because we want results for each team whether they were home or away.  So, we'll create a new DataFrame that organizes the in that way.  First, create a DataFrame called results_1.  You select the following columns from football_results: 'home_team','away_team','home_score','away_score',  and 'date'.  Print out the first 5 lines.
- Next, create a DataFrame called results_2 from results_1.  You rename the column for 'home_team' to 'team', for 'away_team' to 'opponent', for 'home_score' to 'points_for', and for 'away_score' to 'points_against'.  Do not use `inplace=True`.  This dataset gives all the entries for the home teams.  Print out the first 5 lines.
- Next, create a DataFrame called results_3 from results_1.  This also renames the columns, but now the rename is: 'away_team' becomes 'team', 'home_team' becomes 'opponent', 'away_score' becomes 'points_for', and 'home_score' becomes 'points_against'.  This dataset gives all the entries for the away teams.  Print out the first 5 lines.
- Concatenate the results, resetting the index.  Store the result in football_results.  Print out the first 5 lines.  Now we have all the entries per team.
- Do a `groupby()` on 'team'.  Get the mean() of the 'points_against' column.  Store the result (it is a Series) in the variable points_against.
- Sort points_against so the values are descending.  Print out the first 10 lines.  These are the teams that are very bad on defense.

### **Task 10: More Data Wrangling for Football Results**

This time, you'll have to figure out the steps.  Starting with the football_results DataFrame you created in Task 9, print out the most recent 10 games for Tunisia.  Remember to sort these so that you get the right games.  Avoid use of "in_place=True", as you may get annoying warnings.  It is often better to create a new DataFrame and store the result.


### **Submit the Notebook for Your Assignment**  

📌 **Follow these steps to submit your work:**  

#### **1️⃣ Get a Sharing Link for Your Assignment**  
- On the upper right of the Kaggle page, click on Save Version and save, accepting all defaults.  You can just do a quick save.
- On the upper right, click on Share.  Choose Public, make sure that Allow Comments is on, and copy the public URL to your clipboard.

#### **2️⃣ Submit Your Kaggle Link**  
- Paste the URL into the **assignment submission form**.  

---


```

```

### Submission Instructions

Please submit on time

### Checklist

Checklist will be provided when the lesson is generated.

### Check for Understanding

Understanding checks will be provided when the lesson is generated.

## Subsections

### Lesson 5


# **Lesson 05 — Data Wrangling and Aggregation**

## **Lesson Overview**
**Learning objective:** Students will learn to manipulate, summarize, and combine datasets in Pandas using selection, aggregation, merging, and transformation methods. They will practice accessing specific data, performing group-level calculations, and combining data from multiple sources.


### **Topics:**
1. Pandas Review (Optional): Recap of Series, DataFrames, and key methods from Lesson 3.
2. Data Selection: Selecting subsets with `.loc[]`, `.iloc[]`, `.at[]`, and `.iat[]`; filtering rows by conditions; applying string methods.
3. Data Aggregation: Grouping data with `groupby()`; applying functions like `sum()`, `mean()`, and `count()`; using `agg()` for multiple aggregations.
4. Merging and Joining: Combining DataFrames with `merge()` and `join()`; inner, outer, left, and right joins; joining on one or multiple keys.
5. Data Transformation: Adding, updating, and deleting columns; using operators, Series methods, `map()`, and NumPy functions for transformation.
6. Utility Methods: Renaming columns, setting or resetting index, and sorting data.
---

## **4.1 Pandas Review & Deep Dive** *(Optional)*

Last week, we introduced Pandas, a powerful tool for data analysis. If you want a refresher on key Pandas concepts, **[listen to this NotebookLM-generated podcast](https://youtu.be/T46zVBxHrjc) reviewing what we learned last week**. 

*Note: The podcast references two sources, linked below.*

  * (PDF) [Introduction to Pandas](https://github.com/Code-the-Dream-School/python-essentials/blob/ff583aac6befdb1e008b4d149527bc0dd5c437ef/lessons/resources/Pandas%201%20PDF.pdf)
  * (Slide Deck) [Pandas for Dummies](https://www.slideshare.net/slideshow/numpy-and-pandas-introduction-for-beginners/281988048)

## **4.2 Data Selection**

### **Overview**
Indexing and slicing allow you to extract specific rows or columns from a DataFrame, making it easier to analyze subsets of your data.

### **Key Methods:**
- `.loc[]`: Select rows and columns by labels.
- `.iloc[]`: Select rows and columns by integer position.
- `.at[]`: Access a specific cell by label.
- `.iat[]`: Access a specific cell by position.

### **Why Use Data Selection?**
Data selection helps you:
- Filter relevant data for analysis.
- Access specific values or ranges for visualization or calculation.
- Preprocess data by selecting subsets of interest.

**You should run all of the following code examples within the Python interactive shell.**  Start VSCode from within your `python_homework` directory, start a terminal within VSCode, and enter the `python` command to start the shell.

### **Example: Using `.loc[]` and `.iloc[]`**
```python
import pandas as pd

# Sample DataFrame
data = {'Name': ['Alice', 'Bob', 'Charlie', 'David'],
        'Age': [24, 27, 22, 32],
        'Score': [85, 92, 88, 76]}
df = pd.DataFrame(data)

# Select the 'Name' column
print(df['Name'])

# Select rows and specific columns
print(df.loc[0:2, ['Name', 'Age']])

# Select rows by position
print(df.iloc[:2])  # First two rows
```
## **Explanation:**
`.loc[]` is used for label-based indexing. Here, df.loc[0:2, ['Name', 'Age']] selects rows 0 to 2 and the 'Name' and 'Age' columns.
`.iloc[]` is used for position-based indexing. df.iloc[:2] selects the first two rows.

This is slicing, similar to the slicing of lists described in lesson 2.  There are some differences however. The indices for df, in this case, are 0 through 3.

```python
print(df.loc[0:2])  # This prints the first 3 rows! It starts with the row with index 0 and continues up to and including the row with index 2.
print(df.iloc[:2]) # This prints the first 2 rows only.  iloc[] works like list slicing.  It does not include the row with index 2.
print(df.loc[[0,2]]) # This prints row 0 and row 2.  You specify a list of the rows you want.  You can't do this with lists!
```
In each of the cases above, what is returned is a new DataFrame that is a subset of the old one.

One can also specify a filter.  For example:

```python
print(df[df['Age'] > 24])
# print(df[df['Age'] > 24 and df['Score'] >=88])         Doesn't work!  'and' is not a valid operator for Series!
print(df[(df['Age'] > 24) & (df['Score'] >=88)])        # This one does work! It does the boolean AND of corresponding series elements.
# print(df["a" in df['Name']])                          Doesn't work!  The "in" operator doesn't work for Series!
print(df[df['Name'].str.contains("a")])                 # This does work!  
# There are a bunch of useful str functions for Series.  While we're at it:
# df['Name'] = df['Name'].upper()                       Doesn't work!!
df['Name'] = df['Name'].str.upper()                     # Does work! 
print(df)
```


## **4.3 Data Aggregation**

### **Overview**
Aggregating data involves summarizing it by groups, enabling insights at a higher level (e.g., total sales by region, average score by category).

### **Key Method:**
- `groupby()`: Groups data by one or more columns.
- Aggregation functions: `sum()`, `mean()`, `count()`, etc.

### **Why Use Aggregation?**
Aggregation simplifies data analysis by:
- Summarizing patterns across categories.
- Providing key metrics like totals, averages, and counts.
- Reducing data complexity.

### **Example: Using `groupby()`**
```python
# Group data by a column and calculate the sum
data = {'Category': ['A', 'B', 'A', 'B', 'C'],
        'Values': [10, 20, 30, 40, 50]}
df = pd.DataFrame(data)

# Group by 'Category' and calculate the sum
grouped = df.groupby('Category').sum()
print(grouped) # grouped is another DataFrame with summary data

# Calculate the mean for each group
mean_values = df.groupby('Category')['Values'].mean()
print(mean_values)
```
## Explanation: 
- **`df.groupby('Category').sum()`** groups the data by the 'Category' column and calculates the sum of 'Values' within each category.
- **`df.groupby('Category')['Values'].mean()`** calculates the mean of 'Values' for each category.

---

### **Advanced Aggregation**

You can apply multiple aggregation functions at once by using `agg()`. This allows you to calculate various summary statistics for each group.

#### Example: Applying Multiple Aggregations

```python
import pandas as pd

# Sample DataFrame
data = {'Category': ['A', 'B', 'A', 'B', 'C'],
        'Values': [10, 20, 30, 40, 50]}
df = pd.DataFrame(data)

# Group by 'Category' and apply multiple aggregation functions
result = df.groupby('Category').agg({'Values': ['sum', 'mean', 'count']})
print(result)
```

## **Explanation:**

`sum()` calculates the total sum of values for each category.
`mean()` calculates the average value for each category.
`count()` counts the number of non-null entries for each category

Note: For a given agg() invocation on a column, you can specify one or several aggregation functions:

```python
result1 = df.groupby('Category').agg({'Values': 'sum'})
# or
result2 = df.groupby('Category').agg({'Values': ['sum', 'mean', 'count']})
```
If you print out result1 and result2, you'll see that they look different.  The result2 DataFrame has column headers with several rows, because 3 columns are needed for Values aggregation, one for some, one for mean, and one for count.  The column names in this case are tuples, such as `("Values","sum").

In the result1 case, you just have one column for the sum of values, and the column name is "Values".  The difference hangs on whether you specify a single aggregation function or a list.

## **4.4 Merging and Joining**

### **Overview**
Combine multiple DataFrames using shared keys (columns or indices). 

### **Key Methods:**
- `merge()`: Combines DataFrames on common columns.
- `join()`: Combines DataFrames based on their indices.

### **Why Use Merging and Joining?**
- Combine related datasets for comprehensive analysis.
- Handle data stored across multiple sources.
- Maintain relationships between data records.

### **Example: Using `merge()`**
```python
# Sample DataFrames
df1 = pd.DataFrame({'ID': [1, 2, 3], 'Name': ['Alice', 'Bob', 'Charlie']})
df2 = pd.DataFrame({'ID': [1, 2, 4], 'Score': [85, 92, 88]})

# Merge on the 'ID' column
merged_df = pd.merge(df1, df2, on='ID', how='inner')
print(merged_df)  # Inner merge
```

The merged DataFrame has the columns from both DataFrames.  In this case the key is the 'ID' column.  If those match up, the rows of the merged DataFrame will have both 'Name' and 'Score' columns.

Suppose that the two DataFrames also both have an 'Age' column.  You end up with an `Age_x` and an `Age_y` columns, where the renaming is done to prevent collision.  There are ways to choose which one you want to keep.

This is an inner merge.  That means you get only the rows where the ID values match.  One could specify a `how` value of 'left', 'right', or 'outer'.  'left' means include all rows from the left DataFrame, along with matching rows from the right DataFrame.  'right' means the converse.  And 'outer' means include all rows, matching up the ones for which the 'ID' is the same.  When using 'left', 'right', or 'outer', you get `NaN` values in the columns to be added for rows that don't match up.
### Merging on Multiple Columns

Sometimes you need to merge two DataFrames based on multiple columns. This is useful when you have composite keys or want to match on more than one condition.

```python
import pandas as pd

# Sample DataFrames

df1 = pd.DataFrame({
    'ID': [1, 2, 3],
    'Date': ['2021-01-01', '2021-01-02', '2021-01-03'],
    'Name': ['Alice', 'Bob', 'Charlie']
})

df2 = pd.DataFrame({
    'ID': [1, 2, 3],
    'Date': ['2021-01-01', '2021-01-02', '2021-01-03'],
    'Score': [85, 92, 88]
})

# Merge on both 'ID' and 'Date'
merged_df = pd.merge(df1, df2, on=['ID', 'Date'], how='inner')
print(merged_df)
```
In this example:

Merging on both 'ID' and 'Date': This allows you to ensure that the rows are only merged when both conditions match, i.e., the same ID and the same Date.
how='inner': This ensures that only the rows with matching values in both DataFrames are included in the result.

## **Explanation:** 
The merge() function combines two DataFrames based on a common column. Here, it's merging df1 and df2 on the 'ID' column using an inner join, meaning only rows with matching 'ID' values from both DataFrames will appear in the result.  You can also use the join() function.  This matches on index values, instead of the values in one or several key columns.

### **Example: Using `join()`**
```python
# Join DataFrames by index
df1 = pd.DataFrame({'Name': ['Alice', 'Bob', 'Charlie']}, index=[1, 2, 3])
df2 = pd.DataFrame({'Score': [85, 92, 88]}, index=[1, 2, 4])

joined_df = df1.join(df2, how='outer')
print(joined_df)
```

## **Data Transformation**

While one can do transformation of the DataFrame as a whole, for the moment we will focus on approaches that do it one column at a time.  You can add, replace, or delete a column of a DataFrame at any time.

```python
joined_df['bogus']=['x','y','z','w'] # adds a column
print(joined_df)
joined_df['bogus']=joined_df['bogus'] + "_value"  # replaces a column
print(joined_df)
joined_df.drop('bogus', axis=1, inplace=True) # deletes the column.  You need axis=1 to identify that the drop is for a column, not a row
print(joined_df)
```

Look carefully at the case where the column is replaced.  `joined_df['bogus']` returns a view of the column, which is a Series.  You don't write to that directly.  You create a new column, transforming the existing value.  In this case, "_value" is concatenated to each of the values in the original view.  Then, you replace the 'bogus' column with the new column.

You can transform a Series in several ways.
- You can use an operator, as in the above example.  Of course, you can't raise a string to a power of 2, or anything like that, so the type of the entry is important.
- You can use a Series method.  One important example is the map() method, but there are others, such as astype().
- You can use a NumPy function that can operate on a Series.  
Let's look at an example of each:

```python
import numpy
data = {'Name': ['A','B','C'],'Value':[1,2,3]}
new_df = pd.DataFrame(data)
print(new_df)
new_df['Value'] = new_df['Value'] ** 2  # using an operator
print(new_df)
new_df['Value'] = numpy.sqrt(new_df['Value']) # using a numpy function.  You can't use math.sqrt() on a Series.
print(new_df)
new_df['EvenOdd'] = new_df['Value'].map(lambda x : 'Even' if x % 2 == 0 else 'Odd') # the map method for a Series
print(new_df)
new_df['Value'] = new_df['Value'].astype(int) # type conversion method for a Series
print(new_df)
```
The map() method takes one parameter, a function that does the conversion.  In the example above, a lambda is used to specify the function, and a ternary expression is used in the lambda.

## **Utility Methods**

### **Changing Column Names**

You can rename one or more columns as follows:

```python
joined_df.rename(columns={'Score':'Test Score'}, inplace=True)
print(joined_df)
```

### **Converting a Column To An Index**

```python
renamed_df=joined_df.set_index('Name')
print(renamed_df)
```

### **Sorting a DataFrame**

You can sort a DataFrame by column values: 

```python
joined_df.sort_values(by='Score',ascending=False,inplace=True)
print(joined_df)
```

### **Resetting the Index***

After you sort, the index values are no longer in order.  In this and other cases, you may want to reset the index:

```python
joined_df.reset_index(inplace=True, drop=True)
print(joined_df)
```

---

## **Check for Understanding**

1. **How can you select rows where the "Age" column is greater than 25?**
   - A) `df.loc[df['Age'] > 25]`
   - B) `df.iloc[df['Age'] > 25]`
   - C) `df[['Age'] > 25]`
   - D) `df[df['Age'] > 25]`

2. **Which method is used to combine two DataFrames on their indices?**
   - A) `join()`
   - B) `merge()`
   - C) `groupby()`
   - D) `concat()`


<details>

<summary>Answer</summary>

**Answer Key:**
1. A or D  
2. A  

</details>
---

## **Summary**

In this lesson, you’ve learned:
- How to select and slice subsets of data using `.loc[]` and `.iloc[]`.
- How to use `groupby()` for aggregations like `sum()` and `mean()`.
- How to combine DataFrames using `merge()` and `join()`.
- How to transform the data.
- Some utilities to rename columns, sort, convert a column to an index, and reset the index.

Use these techniques to perform advanced data analysis in Pandas. For further exploration, refer to the [Pandas Documentation](https://pandas.pydata.org/docs/) and Python's [official documentation](https://docs.python.org/3/).
```


**Video URL:** No video available

**Code Examples:**

No code examples available

**External Links:**

No external links available

**Quizzes:**

No quizzes available

## Supplemental Videos

No supplemental videos available

## References

No references available

## Podcast URL

No podcast available
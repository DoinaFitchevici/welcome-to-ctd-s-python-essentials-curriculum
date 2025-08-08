# Lesson 2 — Data Structures and File Handling

## Overview

No overview provided

## Learning Objectives

- Students will explore various data structures, such as lists, tuples, dictionaries, and sets. They will learn how to read and write data to files and use external modules.  Additionally, they will be introduced to basic OS operations and using virtual environments.

## Topics Covered

- * Lists, Tuples, Dictionaries, and Sets: Creating, accessing, and modifying data structures.
- * File Handling: Reading from and writing to text and CSV files.
- * Introduction to Modules & packages: Importing and using Python libraries.
- * Keyboard Input
- * Working with the OS: Interacting with the file system and executing commands.
- * Virtual Environments: Managing dependencies for Python projects.

## Status

pending

## Assignment

Assignment for Lesson 2

### Objective

No objective specified

### Expected Capabilities

Expected capabilities will be defined as the lesson progresses.

### Instructions

Instructions will be provided when the lesson is generated.

### Tasks

#### Task 1: Task 1

## Lesson 2 Assignment: Data Structures and File Handling

**Objective:** In this assignment, you practice the use of the input() function.  You also practice file operations.  You use several methods of the list class, and you construct dictionaries from the contents of a CSV file.

### **Step 1: Complete the Coding Tasks**  

Homework for this assignment is created within your `python_homework` folder.  Be sure to create an `assignment2` branch.  Then, write Python code to complete the following tasks.  As you do, remember to put in **comment lines to mark your code for Task 1, Task 2, and so on.**

**Help is Available**

You may find these tasks a little challenging.  If you get stuck, 1:1 mentors are available to answer your questions.  Appointments are available in the [1:1 Mentor Table](https://airtable.com/appoSRJMlXH9KvE6w/shrQinGb1phZYwdiL)

On Windows, if you find that the prompt in git bash is unexpected, you can fix it by running ``cd \`pwd``.

Since Python uses indentation to define blocks of code, it is often necessary to indent or outdent a whole block of code.  You can do this in vscode by selecting the code and then typing `ctl-]` to indent or `ctl-[` to outdent.


---

### **Task 1: Diary**

1. Change to the `assignment2` folder of your `python_homework` folder.  You create your programs for the assignment in this folder.

2. Create a program called `diary.py`. Add code to do the following:
   - Open a file called `diary.txt` for appending.
   - In a loop, prompt the user for a line of input.  The first prompt should say, "What happened today? ".  All subsequent prompts should say "What else? "
   - As each line is received, write it to `diary.txt`, with a newline (`\n`) at the end.
   - When the special line "done for now" is received, write that to `diary.txt`.  Then close the file and exit the program (you just exit the loop).
   - Wrap all of this in a try block. If an exception occurs, catch the exception and print out "An exception occurred." followed by the name of the exception itself. Now, normally, you catch specific types of exceptions, and handle each according to program logic.  In this case, you can catch any non-fatal exceptions via an except for `Exception`, and then display the information from the exception and exit the program.  The `traceback` module provides a way to include function traceback information in your error message, which will make it easier to find the error.  You can use the following code to handle exceptions using the traceback module.
   ```python
   import traceback

   ...

   except Exception as e:
      trace_back = traceback.extract_tb(e.__traceback__)
      stack_trace = list()
      for trace in trace_back:
         stack_trace.append(f'File : {trace[0]} , Line : {trace[1]}, Func.Name : {trace[2]}, Message : {trace[3]}')
      print(f"Exception type: {type(e).__name__}")
      message = str(e)
      if message:
         print(f"Exception message: {message}")
      print(f"Stack trace: {stack_trace}")
   ```
   - Open the file using a `with` statement (inside the try block), and rely on that statement to handle the file close.
   - The input statement should be inside the loop inside the `with` block.

3. Test the program.
   - Run it a couple of times to create diary entries. (`python diary.py`)
   - Have a look at `diary.txt` to make sure it appears correct.  **Warning:** `diary.txt` will end up in GitHub when you submit your homework, so don't put in anything personal.
   - Trigger an exception while running the program:  When it prompts you for input, press Ctrl-D.  You may need to type Ctrl-C and newline to trigger an exception if Ctrl-D doesn't work.  Check to see that the exception is handled. 

### **Task 2: Read a CSV File**

This task, and the others that follow below, use the same pattern as for assignment1. This pattern is known as Test Driven Development (TDD).  It is a good practice which is often used in software industry.  You will need to create assignment2.py for the rest of the tasks.  Then type the following command:
```bash
pytest -v -x assignment2-test.py
```
This will give errors to report what you need to fix.  You run it repeatedly as you create the following functions, until all functions are working correctly.

Remember to import the `csv` module for this task.

2. Create a function called read_employees that has no arguments, and do the following within it. 
   - Declare an empty dict.  You'll add the key/value pairs to that.  Declare also an empty list to store the rows.
   - You next read a csv file. Use a try block and a with statement, so that your code is robust and so that the file gets closed.
   - Read `../csv/employees.csv` using csv.reader().  (This csv file is used in a later lesson to populate a database.)
   - As you loop through the rows, store the first row in the dict using the key "fields".  These are the column headers.
   - Add all the other rows (not the first) to your rows list.
   - Add the list of rows (this is a list of lists) to the dict, using the key "rows".
   - The function should return the dict.
   - Add a line below the function that calls read_employees and stores the returned value in a global variable called employees. Then print out this value, to verify that the function works.
   - In this case, it's not clear what to do if you get an exception.  You might get an exception because the filename is bad, or because the file couldn't be parsed as a CSV file.  For now, just use the same approach as described above: catch the exception, print out the information, and exit the program.  One likely exception in this case is an error in the syntax of your code.

3. Run the test to see if you have this much right.

A word about what's going on when the test runs: The test file imports your assignment2.py module.  When the import statement occurs, all the program statements in your module that are outside of functions do run.  That means the statement which sets your employees global variable is run.  As a result, the assignment2-test.py can reference this global variable too -- and it does.  If you forget to set this variable in your program, the test reports an error.

### **Task 3: Find the Column Index**

1. Create a function called column_index.  The input is a string.  The function looks in employees["fields"] (an array of column headers) to find the index of the column header requested.  There won't be much to this function, because you just use the index() method of the list class, like so:
```python
employees["fields"].index("first_name")
```
The index() method returns the index of the matching value from the list.

2. The column_index function should return this index.

3. Run the test again to see if the test passes.

4. Call the column_index function in your program, passing the parameter "employee_id".  Store the column you get back in a variable called employee_id_column.  This global value is used for subsequent steps.

### **Task 4: Find the Employee First Name**

1. Create a function called first_name.  It takes one argument, the row number.  The function should retrieve the value of first_name from a row as stored in the employees dict.

2. You should first call your column_index function to find out what column index you want.

3. Then you go to the requested row as stored in the employees dict, and get the value at that index in the row.

4. Return the value.

5. Try the test again.


### **Task 5: Find the Employee: a Function in a Function**

1. Create a function called employee_find.  This is passed one argument, an integer.  Just call it employee_id in your function declaration. We want it to return the rows with the matching employee_id.  There should only be one, but sometimes a CSV file has bad data.

2. We could do this with a loop.  But we are going to use the filter() function.  Inside the employee_find function (yes, you do declare functions inside functions sometimes), create the following employee_match function:
```python
def employee_match(row):
   return int(row[employee_id_column]) == employee_id
```
This function is referencing the employee_id value that is passed to the employee_find function.  It can access that value because the employee_match function is inside the employee_find function.  Note that we need to do type conversion here, because the CSV reader just returns strings as the values in the roows.  This inner function returns True if there is a match.  We are using the employee_id_column global value you set in Task 3.

3. Now, still within the employee_find function, call the filter() function.  This is another one of those Python free standing functions.  (It is not a method of the list class.)  You call filter() as follows:
```python
matches=list(filter(employee_match, employees["rows"]))
```
The filter() function needs to know how to filter, and the employee_match function provides that information.  The filter() function calls employee_match once per row, saying, Do we want this one?  When the filter function completes, we need to do type conversion to convert the result to a list.

4. The employee_find function then returns the matches.

5. Run the test and see if you got it right.

### **Task 6: Find the Employee with a Lambda**

The employee_match function is a silly one-liner.  Lambdas allow us to give the logic inline.

1. Create a function employee_find_2.  This function does exactly what employee_find does -- but it uses a lambda.
```
def employee_find_2(employee_id):
   matches = list(filter(lambda row : int(row[employee_id_column]) == employee_id , employees["rows"]))
   return matches
```

Note that there is no return statement in the lambda.  There is the parameter passed to the lambda (a row), followed by a colon, followed by the expression that gives the result.

2. Run the test to make sure things still work.


### **Task 7: Sort the Rows by last_name Using a Lambda**

We want to call the sort() method on the rows.  However, we need to tell it which column to use for the sort.

1. Create a function sort_by_last_name.  It takes no parameters.  You sort the rows you have stored in the dict.

2. Within the function, you call employees["rows"].sort().  This sorts the list of rows in place. But, you need pass to the list.sort() method a keyword argument called key (so you pass a parameter with `key=` when you call it).  You set that keyword parameter equal to a lambda.  The lambda is passed the row, and the expression after the colon gives the value from the row to be used in the sort.  You might want to use your column_index function for last_name so you know which value from the row should be given in the lambda expression.  Remember that the `sort()` method sorts the list in place and does not return the sorted list.

3. The sort_by_last_name function returns the sorted list of rows.

4. Run the test until this works.

5. Call the function in your program, and then print out the employees dict, to see it in sorted form.

### **Task 8: Create a dict for an Employee**

1. Create a function called employee_dict.  It is passed a row from the employees dict (not a row number).  It returns a dict.
   - The keys in the dict are the column headers from employees["fields"].
   - The values in the dict are the corresponding values from the row.
   - Do not include the employee_id in the dict.  You skip that field for now.

2. Return the resulting dict for the employee.

3. Add a line to your program that calls this function and prints the result.  Use a row from the rows stored in the employees dict to pass to the function for this test.

4. Get the test working.

If you want to try something extra, look up the `zip()` function, which can be used to simplify the code for this problem.

### **Task 9: A dict of dicts, for All Employees**

1. Create a function called all_employees_dict.
   - The keys in the dict are the employee_id values from the rows in the employees dict.
   - For each key, the value is the employee dict created for that row.  (Use the employee_dict function you created in task 8.)

2. The function should return the resulting dict of dicts.

3. Add a line to your program that calls this function and prints the result.

4. Get the test working.

### **Task 10: Use the os Module**

Sometimes the behavior of a program is to be modified without changing the program itself.  One way is to use environment variables.  Environment variables are also used to store secrets needed by the program, such as passwords.  Environment variables are accessed via the `os.getenv()` function.  Of course, there are many other functions in the os package.

1. Within the terminal, enter the command `export THISVALUE=ABC`.

2. Add a line to `assignment2.py` to import the os module.

3. Create a function get_this_value().  This function takes no parameters and returns the value of the environment variable `THISVALUE`.

4. Get the test working.  (Note that each time you want this test to pass, you have to have the `THISVALUE` environment variable set in your terminal session.)

### **Task 11: Creating Your Own Module**

1. In the same folder, create a file called custom_module.py, with the following contents:

```python
secret = "shazam!"

def set_secret(new_secret):
   global secret
   secret = new_secret
```

2. Add the line `import custom_module` to assignment2.py.

3. Create a function called set_that_secret.  It should accept one parameter, which is the new secret to be set.  It should call custom_module.set_secret(), passing the parameter, so as to set the secret in custom_module.

4. Add a line to your program to call set_that_secret, passing the new string of your choice.

5. In another line, print out custom_module.secret.  Verify that it has the value you expect.

6. Run the test until the next part passes.


### **Task 12: Read minutes1.csv and minutes2.csv**

The "story" behind the following list of tasks is as follows.  A club meets, and for each meeting, there is a chairperson.  The club keeps several notebooks that record who whas the chairperson on a given date.  Some of the information is in one notebook, some in the other.  The club now wants to combine this information, to get the list of chairpersons sorted by date.  But the information in the csv files contains duplicates and is in no particular order.  (Yeah, the story is lame, but it is similar to other data analysis tasks.)

1. Create a function called `read_minutes`.  It takes no parameters.  It creates two dicts, minutes1 and minutes2, by reading `../csv/minutes1.csv` and `../csv/minutes2.csv`.  Each dict has `fields` and `rows`, just as the employees dict had.  However! As you create the list of rows for both minutes1 and minutes2, convert each row to a tuple.  The function should return both minutes1 and minutes2.  **Note** You can return several values from a Python function, as follows: `return v1, v2`.  Don't worry about duplicates yet.  They will be dealt with in later tasks.  Think about the DRY (Don't repeat Yourself principal).  You may want to create a helper function to avoid duplicating code.

2. Call the function within your assignment2.py script.  Store the values from the values it returns in the global variables minutes1 and minutes2. **Note** When a function returns several values, you get them as follows: `v1, v2 = function()`. Print out those dicts, so that you can see what's stored.

3. Run the test until this part passes.

### **Task 13: Create minutes_set**

1. Create a function called `create_minutes_set`.  It takes no parameters. It creates two sets from the rows of minutes1 and minutes2 dicts.  (This is just type conversion.  However, to make it work, each row has to be hashable!  Sets only support hashable elements.  Lists aren't hashable, so that is why you stored the rows as tuples in Task 10.)  Combine the members of both sets into one single set.  (This operation is called a union.)  The function returns the resulting set.

2. Call the function within your assignment2.py script.  Store the value returned in the global variable minutes_set.

3. Run the test until the next part passes.

### **Task 14: Convert to datetime**

1. Add a statement, `from datetime import datetime`, to your program.  The datetime module has some nice capabilities for converting strings to dates.  You can look them up: strptime() and strftime().

2. Create a function called create_minutes_list.  It takes no parameters, and does the following:
   - Create a list from the minutes_set.  This is just type conversion.
   - Use the `map()` function to convert each element of the list.  At present, each element is a list of strings, where the first element of that list is the name of the recorder and the second element is the date when they recorded.
   - The map() should covert each of these into a tuple.  The first element of the tuple is the name (unchanged).  The second element of the tuple is the date string converted to a datetime object.
   - You convert the date strings into datetime objects using `datetime.strptime(string, "%B %d, %Y")`.
   - So, you could use the following lambda:
   `lambda x: (x[0], datetime.strptime(x[1], "%B %d, %Y"))`
   - The function should return the resulting list.

3. Call the function from within your program.  Store the return value in the minutes_list global.  Print it out, so you can see what it looks like.

4. Run the test until the next part passes.

### **Task 15: Write Out Sorted List**

1. Create a function called write_sorted_list.  It takes no parameters.  It should do the following:
   - Sort minutes_list in ascending order of datetime.
   - Call map again to convert the list.  In this case, for each tuple, you create a new tuple.  The first element of the tuple is the name (unchanged).  The second element of the tuple is the datetime converted back to a string, using `datetime.strftime(date, "%B %d, %Y")`
   - Open a file called `./minutes.csv`.  Use a csv.writer to write out the resulting sorted data.  The first row you write should be the value of `fields` the from minutes1 dict.  The subsequent rows should be the elements from minutes_list.
   - The function should return the converted list.

2. Call this function from within your program.  Then check that the file is created, and that it contains appropriate content.

3. Run the test again until the next test has passed.

### Check for Understanding

1. You created the minutes_set from several lists.  You then created a list from the set.  What's the point of the set, if you're going to end up with a list?

2. Why did you subsequently need to create the list called minutes_list?  Couldn't you just keep working with the set?

3. Why did you need to convert the date strings to datetime objects?

4. Why did you convert them back to strings before writing out the CSV?


### Answers

1. The original lists had duplicates.  A set has only unique values, so by converting to a set, you get rid of duplicates.

2. You need to call the map() function and sort() method.  Set objects don't support these, and in fact, the entries in a set are not in any particular order.  So, for these steps, you need lists.

3. You needed to convert the date strings to datetime objects.  Otherwise, they'd just be sorted in alphabetical order, and "April 1, 2023" would come before "September 2, 1980".  You could have done this conversion in the lambda for `key=` in the sort() of the list, but that approach would make that lambda a little complicated.

4. When a datetime object is printed, its appearance is not as friendly as the original date string, so you converted it back.


### **Step 2: Submit Your Assignment on GitHub**  

**Follow these steps to submit your work:**  

#### **1️⃣ Add, Commit, and Push Your Changes**  
- Within your python_homework folder, do a git add and a git commit for the files you have created, so that they are added to the `assignment2` branch.
- Push that branch to GitHub. 

#### **2️⃣ Create a Pull Request**  
- Log on to your GitHub account.
- Open your `python_homework` repository.
- Select your `assignment2` branch.  It should be one or several commits ahead of your main branch.
- Create a pull request.

#### **3️⃣ Submit Your GitHub Link**  
- Your browser now has the link to your pull request.  Copy that link. 
- Paste the URL into the **assignment submission form**.  



```

```

### Submission Instructions

Please submit on time

### Checklist

Checklist will be provided when the lesson is generated.

### Check for Understanding

Understanding checks will be provided when the lesson is generated.

## Subsections

### Lesson 2

# Lesson 2 — Data Structures and File Handling

## 👀 Reminder: How to Follow This Content

* Start by reading the lesson's **learning objective** in the `Lesson Overview` section. Each weekly assignment will measure your skill related to the learning objective.
* Lessons are split into **subsections**, labeled like this: `1.1`, `1.2`, etc.
* Each subsection has a short **supplemental video** that will help you understand the content in that subsection.
* At the end of each subsection, you'll find a multiple-choice **"Check for Understanding"** question. Complete the question and review the material if your answer is not correct!
* After reading through the lesson content and correctly answering the "Check for Understanding" questions, complete the **Weekly Assignment**.

If you have questions at any point, ask a question in the `discussion` Slack channel or reach out to your mentor!

## Lesson Overview

Congrats, you've made it to Lesson 2! This week, we'll deepen our knowledge of core Python concepts, including dictionaries and lists. We'll also learn how to import **modules**, powerful tools that help your Python projects reach their full potential.
Additionally, we’ll learn how to work with the operating system (OS) and virtual environments for more efficient project management.

**Learning objective**: Students will explore various data structures, such as lists, tuples, dictionaries, and sets. They will learn how to read and write data to files and use external modules.  Additionally, they will be introduced to basic OS operations and using virtual environments.

Topics:

* Lists, Tuples, Dictionaries, and Sets: Creating, accessing, and modifying data structures.
* File Handling: Reading from and writing to text and CSV files.
* Introduction to Modules & packages: Importing and using Python libraries.
* Keyboard Input
* Working with the OS: Interacting with the file system and executing commands.
* Virtual Environments: Managing dependencies for Python projects.

## 2.1 Lists, Tuples, Dictionaries, and Sets

Before we talk about lists and tuples, we need to define two new words: "mutable" and "immutable."

Something that is **mutable** can be modified or changed after it is created. Something that is **immutable** cannot be modified or changed after it is created.

Imagine a piece of clay (mutable) versus a ceramic statue (immutable):

* Clay can be reshaped, squished, or molded into different forms after it's first created. You can add or remove parts easily.
* A ceramic statue, once it's fired in a kiln, cannot be changed without breaking it completely.

In Python programming, here's a concrete example using *mutable* lists and *immutable* tuples:

``` python
# Mutable example (list)
fruits = ['apple', 'banana', 'cherry']
fruits.append('date')  # We can add a new item
fruits[0] = 'orange'  # We can change an existing item
print(fruits)  # Now ['orange', 'banana', 'cherry', 'date']

# Immutable example (tuple)
colors = ('red', 'green', 'blue')
# colors[0] = 'yellow'  # This would cause an error
# You cannot change the tuple after creation
```
Strings are also immutable in Python.  This would cause an error:
```
capital = "raleigh"
capital[0] = "R"
```

### Lists

A **list** is a *mutable*, ordered collection of items. Lists allow duplicates and can hold items of different types, although typically you’ll find lists containing items of the same type. You can add, remove, or modify elements in a list, making them versatile for storing data that may change.

```python
fruits = ['apple', 'banana', 'cherry']  # Define a list
fruits.append('orange')  # Add an item
print(fruits)  # Output: ['apple', 'banana', 'cherry', 'orange']
```

#### Key List Methods

* `append(item)`: Adds `item` to the end of the list.
* `remove(item)`: Removes the first occurrence of `item`.
* `sort()`: Sorts the list in place.

There lots of methods and operations which apply to lists including all of the [common](https://docs.python.org/3/library/stdtypes.html#typesseq-common) and [mutable](https://docs.python.org/3/library/stdtypes.html#typesseq-mutable) sequence operations.

A list is an example of an iterable.  So you can iterate on it, as follows:

```python
fruits = ['apple', 'banana', 'cherry']
for fruit in fruits:
    print(fruit)
```
There are various other iterable collections in Python, such as tuples.

#### The map() Function for Lists.

The map() function is not a method of the list class.  It is a Python built in function that operates on iterables. Suppose you have a list of numbers, and you want to increment all of them.  You can do it as follows:

```python
list_one = [3,4,5]
def incrementor(x):
    return x + 1

list_two = list(map(incrementor, list_one)) # [4,5,6]
```

You pass the map() function two arguments, the function that changes the list item, and the iterable itself.  The function returns an iterable, and we can do type coversion to create a list.  Now, the incrementor() function above looks a little stupid.  You'd like to pass something in line, and for that, Python provides:

### Lambdas

```python
list_one = [3,4,5]
list_two = list(map(lambda x: x+1, list_one)) # [4,5,6]
```

The lambda feature is a way to declare a simple function.  Lambdas are, in some respects, similar to arrow functions in JavaScript, but they are much more limited.  A lambda is a simple one liner.  The syntax is as follows: the word `lambda` followed by the arguments to be passed (the map function only passes one parameter, so in the case above there is only argument for the lambda), followed by a colon `:`, followed by an expression.  The value of the expression is what is returned by the lambda.  You can only give one expression in a lambda, so there is no room for multiple statements.

### Slicing Lists

You can create a subset list from a list by slicing.  Here are examples:

```python
list_1 = ['A','B','C','D','E']
list_2 = list_1[1:3] # Slicing from beginning to end. Gives ['B','C'].  list_1[3] is not included.
list_3 = list_1[2:]  # Gives ['C','D','E']
list_4 = list_1[:2]  # Gives ['A', 'B']
list_5 = list_1[-2:] # Gives ['D', 'E'] -- the last two elements

### Tuples

A **tuple** is an *immutable*, ordered collection of items. Once defined, the elements in a tuple cannot be modified, added, or removed. Tuples are useful for data that shouldn’t change, like fixed configuration values or coordinates.

```python
dimensions = (1920, 1080)  # Define a tuple
print(dimensions[0])  # Access the first element: Output: 1920
```

#### Why use tuples?

* Tuples are memory-efficient compared to lists.
* Useful when you want a constant, fixed-size collection of data.

### Dictionaries

A **dictionary** is an unordered collection of key-value pairs. Each key is unique and used to store and retrieve data efficiently. Dictionaries are ideal for mapping relationships, such as a user’s name to their profile data or an item to its price.

```python
person = {'name': 'Jazmine', 'age': 30}  # Define a dictionary
print(person['name'])  # Output: Jazmine
person['email'] = 'jazmine@example.com'  # Add a new key-value pair
```

#### Key Dictionary Methods

* `keys()`: Returns a list of keys in the dictionary.
* `values()`: Returns a list of values.
* `items()`: Returns an iterable over the key, value pairs in the dictionary
* `get(key)`: Returns the value associated with `key`, or `None` if `key` is not found.

The operations and methods available for dictionaries are documented [here](https://docs.python.org/3/library/stdtypes.html#mapping-types-dict).

### Sets

A **set** is an unordered collection of unique elements. Sets are useful for removing duplicates from a list or performing mathematical set operations like union, intersection, and difference.

```python
unique_numbers = {1, 2, 3, 3, 4}  # Define a set (duplicates are ignored)
unique_numbers.add(5)  # Add a new item
print(unique_numbers)  # Output: {1, 2, 3, 4, 5}
```

#### Common Set Operations

* `union()`: Returns a set containing all unique elements from both sets.
* `intersection()`: Returns elements common to both sets.
* `difference()`: Returns elements present in one set but not the other.

Set operations and methods are documented [here](https://docs.python.org/3/library/stdtypes.html#set-types-set-frozenset).

### Review Table: Lists, Tuples, Dictionaries, and Sets

Ok, let's review! Here's a table demonstrating the key differences between the four new terms we just learned:

| Data Structure | Ordered | Changeable (Mutable) | Allows Duplicates | Key-Value Pairs |
|----------------|---------|----------------------|-------------------|-----------------|
| **List**       | Yes     | Yes                 | Yes               | No              |
| **Tuple**      | Yes     | No                  | Yes               | No              |
| **Dictionary** | No      | Yes (Keys: No)      | Keys: No, Values: Yes | Yes           |
| **Set**        | No      | Yes                 | No                | No              |

### 2.1 Video: Lists, Tuples, Dictonaries, and Sets

Video 2.1 explains lists, sets, and tuples. 

**[View the video here](https://youtu.be/gOMW_n2-2Mw?feature=shared).**

### 2.1 Check for Understanding

**Question**: Which of the following statements about Python data structures is correct?

* A) Lists are immutable, and tuples are mutable.
* B) Sets allow duplicate elements.
* C) Dictionaries store data in key-value pairs and do not allow duplicate keys.
* D) Tuples are ordered and changeable.

<details>

<summary>Answer</summary>

**Answer**: C) Dictionaries store data in key-value pairs and do not allow duplicate keys.

</details>

## 2.2 File Handling

In Python, reading from and writing to text files is handled with the `open()` function. Text files are simple, containing plain text data, making them ideal for storing simple logs, configuration data, or notes.

#### Reading a Text File

To read a file, use `open()` with the `"r"` (read) mode and call `.read()`, `.readline()`, or .`readlines()` to get the content.

```python
with open('example.txt', 'r') as file:
    content = file.read()  # Read entire file
    print(content)
```

The python above uses the `with` statement.  This is a way to keep your code looking clean.  You always want to close the file when you are done.  The `with` statement closes it for you on exit from the block.  The file is closed even if there is an exception, but the exception is still passed on to you.  Later in the course, you will also use the `with` statement for a database connection, and it serves the same purpose.

File operations, including the open(), can raise exceptions.  To make your code robust, you put them in a try block, as follows:

```python
try:
    with open('example.txt', 'r') as file:
        content = file.read()  # Read entire file
        print(content)
except Exception as e:
    print(f"An error occurred reading the file: {e}")
else:
    print("The file was read ok.")
```
If your `with` block is longer, you may have other try blocks inside it for more granular exception handling.

#### Writing to a Text File

To write to a file, open it in `"w"` (write) or `"a"` (append) mode. Writing mode will overwrite the file if it exists, while append mode will add to the file.

```python
with open('example.txt', 'w') as file:
    file.write("Hello, World!")  # Write to the file
```

The `write()` method does not add a newline after the string which is provided.  The special character `'\n'` can be added to the end of the string to add a newline.

#### Additional Modes

* `"r+"`: Read and write
* `"a"`: Append to the file (keeps existing content).

### Reading and Writing CSV Files

CSV (Comma-Separated Values) files are commonly used to store tabular data, where each row is a new line, and each value is separated by a comma. Python’s built-in `csv` module makes it easy to work with these files.

#### Reading a CSV File

To read a CSV file, use `csv.reader()` and iterate through the rows.

```python
import csv

with open('example.csv', 'r') as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

#### Writing to a CSV File

To write to a CSV file, use `csv.writer()`. Each row should be a list or tuple representing a row in the CSV.

```python
import csv

with open('example.csv', 'w', newline='') as file:
    writer = csv.writer(file)
    writer.writerow(['Name', 'Age', 'City'])  # Write header row
    writer.writerow(['Jazmine', 30, 'New York'])  # Write a data row
```

#### Additional Options

* `csv.DictReader()` and `csv.DictWriter()`: Use dictionaries to work with row data, which can make reading and writing more convenient when you have headers.

### 2.2 Video: Reading and Writing a CSV File

In this video, we'll demonstrate reading and writing to a real CSV file. After the video, practice reading and writing to a CSV file using the W3 Resource tutorial [here](https://www.w3resource.com/python-exercises/csv/index.php).

**[View the video here](https://youtu.be/MWYRGLKMzAQ?feature=shared).**

### 2.2 Check for Understanding

**Question**: What does the `"w"` mode do when opening a file in Python?

* A) Reads the file without making changes.
* B) Appends new data to the end of the file.
* C) Overwrites the file with new data, creating it if it doesn’t exist.
* D) Opens the file for reading and writing without overwriting.

<details>

<summary>Answer</summary>

**Answer**: C) Overwrites the file with new data, creating it if it doesn’t exist.

</details>

## 2.3 Introduction to Modules

In Python, modules and packages are essential tools for organizing and reusing code. This section will cover everything you need to know about working with both modules and packages effectively.

### Modules

A module is a Python file containing code (functions, classes, and variables) that can be reused across different parts of a project. Modules help with:

1. **Code Organization**: Breaking large codebases into manageable files
2. **Reusability**: Using common code wherever needed
3. **Namespace Management**: Avoiding naming conflicts
4. **Built-in Functionality**: Accessing Python's standard library features

#### Importing Modules

There are several ways to import modules:

```python
# Import entire module
import math
print(math.sqrt(16))  # Output: 4.0

# Import specific functions
from math import sqrt
print(sqrt(16))  # Output: 4.0

# Use aliases for shorter names
import pandas as pd
df = pd.DataFrame({'Name': ['Jazmine', 'Luis'], 'Age': [30, 35]})
```

#### Creating Custom Modules

You can create your own modules by saving Python code in a .py file:

```python
# math_tools.py
def add(a, b):
    return a + b

def multiply(a, b):
    return a * b

# main.py
import math_tools
print(math_tools.add(2, 3))  # Output: 5
```

### Packages

A package is a collection of related modules organized in a directory structure. Packages require an `__init__.py` file to mark the directory as a Python package.  In this course, we don't create large projects with many modules, but as a Python professional, you will need to do this.  The contents of `__init__.py` are not described in this lesson, but you can view [this tutorial](https://packaging.python.org/en/latest/tutorials/packaging-projects/) to see how it is to be done (this is optional for this course).

#### Package Structure Example
```
my_package/
    __init__.py         # Makes this directory a package
    math_tools.py       # Module for math operations
    string_tools.py     # Module for string operations
```

#### Using Packages

```python
# Import specific modules from a package
from my_package import math_tools
print(math_tools.add(10, 20))

# Import specific functions (if configured in __init__.py)
from my_package import add, multiply
```

### Types of Modules

1. **Standard Library**: Provides a vast library of modules and infrastructure.  It is documented [here](https://docs.python.org/3/library/index.html). Examples of built-in modules include:
   - `datetime` for dates and times
   - `json` for JSON data
   - `os` for operating system operations

2. **External Libraries**: Additional modules installed via pip:
   ```bash
   pip install requests
   
   # Then use in code:
   import requests
   response = requests.get('https://api.example.com/data')
   ```

### 2.3 Video: Python Modules and Libraries

What are Python modules? How do you import and work with them? Check out vido 2.3 to learn more. 

**[View the video here](https://youtu.be/XcfxkHrHTVE?feature=shared).**

### 2.3 Check for Understanding

**Question**: Which of the following commands correctly imports only the sqrt function from the `math` module?

* A) `import sqrt from math`
* B) `from math import sqrt`
* C) `import math.sqrt`
* D) `import math as sqrt`

<details>

<summary>Answer</summary>

**Answer**: B) `from math import sqrt`

</details>

## 2.4 Keyboard Input

In Python, handling keyboard input is straightforward, making it easy to interact with users. The input() function is the main way to capture user input from the keyboard, which you can then use directly or store in a variable for further processing.

#### Using `input()`

The `input()` function displays a prompt (optional) and waits for the user to type something and press Enter. By default, `input()` captures the input as a string, so if you need it in another format (like an integer), you’ll have to convert it.

```python
name = input("Enter your name: ")  # Displays a prompt and waits for input
print(f"Hello, {name}!")  # Greets the user with their input
```

#### Converting Input Types

Since `input()` returns data as a string, you’ll often want to convert it for calculations or comparisons.

```python
age = input("Enter your age: ")  # Gets input as a string
age = int(age)  # Converts input to an integer
print(f"Next year, you will be {age + 1} years old.")
```

If the user types something that can’t be converted (e.g., entering "twenty" instead of "20"), this will raise an error. To handle this gracefully, you can use `try-except`:

```python
try:
    age = int(input("Enter your age: "))
    print(f"Next year, you will be {age + 1} years old.")
except ValueError:
    print("Please enter a valid number.")
```

### Example: Simple Calculator Using Keyboard Input

Here’s a basic example that combines multiple `input()` calls to create a calculator. Pay attention to this code, because you'll be creating a calculator in this week's assignment!

```python
# Simple calculator
try:
    num1 = float(input("Enter the first number: "))
    num2 = float(input("Enter the second number: "))
    operation = input("Enter an operation (+, -, *, /): ")

    if operation == "+":
        print("Result:", num1 + num2)
    elif operation == "-":
        print("Result:", num1 - num2)
    elif operation == "*":
        print("Result:", num1 * num2)
    elif operation == "/":
        print("Result:", num1 / num2)
    else:
        print("Invalid operation")
except ValueError:
    print("Please enter valid numbers.")
except ZeroDivisionError:
    print("Cannot divide by zero.")
```

### 2.4 Check for Understanding

**Question**: Which of the following statements about `input()` in Python is correct?

* A) `input()` captures user input and automatically converts it to an integer.
* B) `input()` displays a prompt and captures user input as a string by default.
* C) `input()` captures user input but only works with numbers.
* D) `input()` is used to output text to the console.

<details>

<summary>Answer</summary>

**Answer**: B) input() displays a prompt and captures user input as a string by default.

</details>

## 2.5 Working with the OS

The `os` module in Python provides a powerful interface for interacting with the operating system. It enables you to perform various tasks, including:

* File and directory manipulation
* Environment variable handling
* Running system commands

These functionalities are essential for automating processes and managing files within Python programs.

### Common os Module Functions

**Getting the Current Working Directory**

The `os.getcwd()` function retrieves the path of the current working directory (the directory from which your Python script is executing).

```python
import os
current_directory = os.getcwd()
print(f"Current working directory: {current_directory}")
```

**Changing the Current Working Directory**

You can change the current working directory using `os.chdir(path)`, where `path` specifies the directory you want to switch to.

```python
os.chdir('/path/to/your/folder')
print(f"New working directory: {os.getcwd()}")
```

**Listing Files in a Directory**

The `os.listdir()` function returns a list containing all files and folders within the specified directory.

```python
files = os.listdir('/path/to/your/folder')
print(f"Files in the directory: {files}")
```

**Creating and Removing Directories**

Use `os.mkdir()` to create a new directory and `os.rmdir()` to remove an empty directory.

```python
# Create a new directory
os.mkdir('new_folder')

# Remove the directory
os.rmdir('new_folder')
```

*Note: If the directory isn't empty, you'll encounter an error. To remove a non-empty directory, use `shutil.rmtree()` from the `shutil` module.*

**Checking if a Path Exists**

Use `os.path.exists()` to verify if a file or directory exists at the specified path.

```python
if os.path.exists('some_file.txt'):
    print("The file exists.")
else:
    print("The file does not exist.")
```

**Getting File Information**

The `os.path` module provides functions to check file properties. For instance, use `os.path.isfile()` to determine if a path points to a file and `os.path.isdir()` to check if it's a directory.

```python
if os.path.isfile('some_file.txt'):
    print("This is a file.")
elif os.path.isdir('some_folder'):
    print("This is a folder.")
```

**Executing Shell Commands**

The `os.system()` function allows you to execute shell commands from within your Python program. You can leverage this functionality to run system commands like `ls` or `dir` to list files or execute other commands provided by your operating system.

```python
os.system('ls')  # For Linux/Mac
os.system('dir')  # For Windows
```

*Keep in mind that `os.system()` doesn't return the output of the command. If you need the output, consider using `subprocess.run()` instead.*

**Environment Variables**

You can access environment variables using `os.environ`. For example, to retrieve the `PATH` environment variable:

```python
path_variable = os.environ.get('PATH')
print(path_variable)
```

**Addendum: The sys Package**

In many environments, Python is used as a scripting tool.  Python scripts are invoked with arguments.  The user might type:

```bash
python loadfile.py ./current.csv
```
and the script might load the contents of the file into a database.  The sys package enables this (among other things).  Consider the following code:

```python
import sys
for arg in sys.argv:
    print(arg)  # arg[0] is the program name.  The other arguments are what was passed on the command line.
```

The [argparse](https://docs.python.org/3/library/argparse.html#module-argparse) module provides a powerful framework for handling command line arguments.

### Video 2.5: Working with `os`

**[Watch an overview of working with the `os` module here](https://youtu.be/tJxcKyFMTGo?feature=shared).**

---

## 2.6 Virtual Environments

Virtual environments are a cornerstone of Python development, particularly when managing dependencies and isolating project environments. A virtual environment creates an isolated Python environment, enabling you to have project-specific dependencies that won't interfere with other projects or system-wide Python packages.

### Why Use Virtual Environments?

* **Isolation**: Virtual environments ensure that each project has its own set of dependencies, preventing version conflicts.
* **Reproducibility**: Virtual environments make it simpler to reproduce the exact setup for a project on another machine.
* **Dependency Management**: You can install and update packages without affecting other projects or your system's Python installation.

### Setting Up a Virtual Environment

1. **Install `virtualenv` (optional)**

   While Python 3.3+ comes with the `venv` module for creating virtual environments, some users prefer using `virtualenv` for additional features. To install it:

   ```bash
   pip install virtualenv
   ```

2. **Create a Virtual Environment**

   You can create a virtual environment using either `venv` (built-in module) or `virtualenv` (third-party package).

   - **Using `venv`**:

     ```bash
     python3 -m venv myenv
     ```

     This command creates a directory named `myenv` that contains the virtual environment.  (Note: by convention, `.venv` is usually used as the name of the virtual environment, instead of `myenv` as in this example.)

   - **Using `virtualenv`**:

     ```bash
     virtualenv myenv
     ```

   **In both cases, `myenv` is the directory where the isolated Python environment will live.**

3. **Activating the Virtual Environment**

   To activate the virtual environment, use the following commands:

   * **Windows:**
     The following command assumes that you are using Git Bash as your Windows development terminal environment.  This is strongly recommended.

     ```bash
     source myenv/Scripts/activate
     ```



   * **Mac/Linux:**

     ```bash
     source myenv/bin/activate
     ```

   Once activated, your terminal prompt will usually change to show the virtual environment's name, e.g., `(myenv)`.

4. **Installing Packages in the Virtual Environment**

   After activation, you can install packages as usual with `pip`. These packages will be installed inside the virtual environment, not globally.

   ```bash
   pip install requests
   ```

   This ensures that the `requests` package is available only in the current virtual environment.

5. **Deactivating the Virtual Environment**

   To exit the virtual environment and return to the global Python environment, simply run:

   ```bash
   deactivate
   ```

6. **Managing Dependencies with `requirements.txt`**

   To record all the dependencies installed in your virtual environment, use the `pip freeze` command to generate a `requirements.txt` file:

   ```bash
   pip freeze > requirements.txt
   ```

   This file can be used to recreate the environment on another machine:

   ```bash
   pip install -r requirements.txt
   ```

7. **Virtual Environment with IDEs**

   Many IDEs, like VS Code and PyCharm, allow you to configure the Python interpreter to use the virtual environment. This ensures that the IDE uses the correct Python environment with all the necessary packages installed.

### Video 2.6: The Virtual Environment

Check out Video 2.6 for a quick overview of setting up a virtual environment for Python in VS Code.  Note that you have already done this!  Your python_homework directory uses a virtual environment.

**[Watch the video here](https://youtu.be/GZbeL5AcTgw?feature=shared).**

## 🥳 That's it for Lesson 2!

Check out this week's coding assignment, and reach out to a mentor if you need help!

---
This content was written by Janet Zulu, Reid Russom, and CTD volunteers—with special thanks to the brain trust of John McGarvey, Rebecca Callari-Kaczmarczyk, Tom Arns, and Josh Sternfeld. To submit feedback, please fill out the **[CTD Curriculum Feedback Form](https://forms.gle/RZq5mav7wotFxyie6)**.



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
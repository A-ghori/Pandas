# Titanic Data Analysis with Pandas

This project demonstrates how to use Pandas for data analysis, using the Titanic dataset. Each code block is explained in detail for learning purposes.

---

## 1. **Setup and Installation**

Install Pandas and Openpyxl (for Excel file support):

```python
!pip3 install pandas
!pip3 install pandas
import sys
!{sys.executable} -m ensurepip --upgrade
!{sys.executable} -m pip install pandas
import sys

print(sys.version)          # Shows Python version
print(sys.path)             # Shows all importable paths
print(sys.platform)         # Tells OS (e.g., 'darwin' for macOS)
print(sys.argv)             # Command line args (in scripts)

# openpyxl is a Python library used for:
#   • Reading and writing Excel .xlsx files.
!pip3 install openpyxl
```
**Explanation:**  
- Installs required libraries.
- Shows system info for debugging and environment checks.

---

## 2. **Testing Pandas Installation**

```python
import pandas as pd

# Create test data using dictionary
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 22],
    'City': ['Kolkata', 'Mumbai', 'Delhi']
}

# Convert dictionary to DataFrame
df = pd.DataFrame(data)

# Show the DataFrame
print(df)

# Access a column
print("Names:\n", df['Name'])

# Filter rows where Age > 23
print("Age > 23:\n", df[df['Age'] > 23])
```
**Explanation:**  
- Creates a simple DataFrame to verify Pandas is working.
- Shows basic DataFrame operations: creation, column access, filtering.

---

## 3. **Mini Titanic DataFrame Example**

```python
import pandas as pd
df = pd.DataFrame(
    {
        "Name": [
            "Braund , Mr. Owen Harris",
            "Allen, Mr. William Henry",
            "Bonnell, Miss. Elizabeth",
        ],
        "Age": [
            22,
            35,
            58
        ],
        "Sex": ["male", "male", "female"],
    }
)
df
df.head()  # Display the first few rows of the DataFrame
df.tail()  # Display the last few rows of the DataFrame

# df["Age"]

# df.info()

# When selecting a single column of a pandas DataFrame, the result is a pandas Series.
ages = pd.Series([20, 10, 11], name="Age")
ages
df["Age"].max()  # Get the maximum age
df["Age"].min()  # Get the minimum age
ages.max()       # Get the maximum ages from the Series

df.describe()    # Get a summary of statistics for the DataFrame
```
**Explanation:**  
- Shows how to create a DataFrame from a dictionary.
- Demonstrates `.head()`, `.tail()`, column selection, and summary statistics.

---

## 4. **Titanic Dataset Analysis**

### 4.1. **Load the Titanic CSV**

```python
import pandas as pd
titanic = pd.read_csv("/Users/user/Desktop/Developer/jupyter/Pandas/Titanic-Dataset.csv")
```
**Explanation:**  
- Loads the Titanic dataset from CSV.

---

### 4.2. **Clean Column Names**

```python
titanic.columns = titanic.columns.str.strip().str.lower()
# Removes unwanted leading/trailing spaces and makes all column names lowercase.
```

---

### 4.3. **Convert Age to Numeric**

```python
titanic["age"] = pd.to_numeric(titanic["age"], errors="coerce")
# Converts non-numeric age values to NaN for analysis.
```

---

### 4.4. **Explore the Data**

```python
# Display the first few rows
titanic.head(8)

# Summary statistics
titanic.describe()

# DataFrame info
titanic.info()

# Display the last few rows
titanic.tail()
```
**Explanation:**  
- `.head()`, `.tail()` show sample rows.
- `.describe()` gives statistics.
- `.info()` shows column types and missing values.

---

### 4.5. **Export to Excel and Reload**

```python
titanic.to_excel("titanic.xlsx", sheet_name="passengers", index=False)
titanic = pd.read_excel("titanic.xlsx", sheet_name="passengers")
titanic.info()
```
**Explanation:**  
- Saves DataFrame to Excel, then reloads it to verify.

---

### 4.6. **Age Analysis**

```python
ages = titanic["age"]
ages
ages.head()
titanic.dtypes # Display the data types of each column

type(titanic["age"]) # Check the type of the "Age" column (should be pandas.core.series.Series)

titanic["age"].max()
titanic["age"].shape # Number of elements in "age" column
```
**Explanation:**  
- Shows how to access, inspect, and analyze the "age" column.

---

### 4.7. **Filter Passengers Above Age 35**

```python
above_35 = titanic[titanic["age"] > 35]
above_35.head()

titanic["age"] > 35
```
**Explanation:**  
- Filters passengers older than 35.

---

### 4.8. **Find Missing Ages**

```python
titanic[titanic["age"].isna()]  # Display rows where "Age" is NaN (missing values)
```
**Explanation:**  
- Finds passengers with unknown age.

---

### 4.9. **Filter by Passenger Class**

```python
class_23 = titanic[titanic["pclass"].isin([2, 3])]  # Filter passengers in classes 2 and 3
print(class_23.head())
print(titanic['pclass'].unique())

class_23 = titanic[(titanic["pclass"] == 2) | (titanic["pclass"] == 3)]
print(titanic["pclass"].unique())
```
**Explanation:**  
- Filters passengers by class (2 or 3).

---

### 4.10. **Filter Rows Where Age Is Not NaN**

```python
age_no_na = titanic[titanic["age"].notna()]  # Filter rows where "Age" is not NaN
age_no_na.head()
age_no_na.shape
```
**Explanation:**  
- Keeps only rows with known age.
- `.shape` shows the number of rows and columns in the filtered DataFrame.

---

## **Summary**

- This notebook covers Pandas basics, data cleaning, filtering, and analysis using the Titanic dataset.
- Each code line is explained for clarity.# Titanic Data Analysis with Pandas

This project demonstrates how to use Pandas for data analysis, using the Titanic dataset. Each code block is explained in detail for learning purposes.

---

## 1. **Setup and Installation**

Install Pandas and Openpyxl (for Excel file support):

```python
!pip3 install pandas
import sys
!{sys.executable} -m ensurepip --upgrade
!{sys.executable} -m pip install pandas
import sys

print(sys.version)          # Shows Python version
print(sys.path)             # Shows all importable paths
print(sys.platform)         # Tells OS (e.g., 'darwin' for macOS)
print(sys.argv)             # Command line args (in scripts)

# openpyxl is a Python library used for:
#   • Reading and writing Excel .xlsx files.
!pip3 install openpyxl
```
**Explanation:**  
- Installs required libraries.
- Shows system info for debugging and environment checks.

---

## 2. **Testing Pandas Installation**

```python
import pandas as pd

# Create test data using dictionary
data = {
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Age': [25, 30, 22],
    'City': ['Kolkata', 'Mumbai', 'Delhi']
}

# Convert dictionary to DataFrame
df = pd.DataFrame(data)

# Show the DataFrame
print(df)

# Access a column
print("Names:\n", df['Name'])

# Filter rows where Age > 23
print("Age > 23:\n", df[df['Age'] > 23])
```
**Explanation:**  
- Creates a simple DataFrame to verify Pandas is working.
- Shows basic DataFrame operations: creation, column access, filtering.

---

## 3. **Mini Titanic DataFrame Example**

```python
import pandas as pd
df = pd.DataFrame(
    {
        "Name": [
            "Braund , Mr. Owen Harris",
            "Allen, Mr. William Henry",
            "Bonnell, Miss. Elizabeth",
        ],
        "Age": [
            22,
            35,
            58
        ],
        "Sex": ["male", "male", "female"],
    }
)
df
df.head()  # Display the first few rows of the DataFrame
df.tail()  # Display the last few rows of the DataFrame

# df["Age"]

# df.info()

# When selecting a single column of a pandas DataFrame, the result is a pandas Series.
ages = pd.Series([20, 10, 11], name="Age")
ages
df["Age"].max()  # Get the maximum age
df["Age"].min()  # Get the minimum age
ages.max()       # Get the maximum ages from the Series

df.describe()    # Get a summary of statistics for the DataFrame
```
**Explanation:**  
- Shows how to create a DataFrame from a dictionary.
- Demonstrates `.head()`, `.tail()`, column selection, and summary statistics.

---

## 4. **Titanic Dataset Analysis**

### 4.1. **Load the Titanic CSV**

```python
import pandas as pd
titanic = pd.read_csv("/Users/user/Desktop/Developer/jupyter/Pandas/Titanic-Dataset.csv")
```
**Explanation:**  
- Loads the Titanic dataset from CSV.

---

### 4.2. **Clean Column Names**

```python
titanic.columns = titanic.columns.str.strip().str.lower()
# Removes unwanted leading/trailing spaces and makes all column names lowercase.
```

---

### 4.3. **Convert Age to Numeric**

```python
titanic["age"] = pd.to_numeric(titanic["age"], errors="coerce")
# Converts non-numeric age values to NaN for analysis.
```

---

### 4.4. **Explore the Data**

```python
# Display the first few rows
titanic.head(8)

# Summary statistics
titanic.describe()

# DataFrame info
titanic.info()

# Display the last few rows
titanic.tail()
```
**Explanation:**  
- `.head()`, `.tail()` show sample rows.
- `.describe()` gives statistics.
- `.info()` shows column types and missing values.

---

### 4.5. **Export to Excel and Reload**

```python
titanic.to_excel("titanic.xlsx", sheet_name="passengers", index=False)
titanic = pd.read_excel("titanic.xlsx", sheet_name="passengers")
titanic.info()
```
**Explanation:**  
- Saves DataFrame to Excel, then reloads it to verify.

---

### 4.6. **Age Analysis**

```python
ages = titanic["age"]
ages
ages.head()
titanic.dtypes # Display the data types of each column

type(titanic["age"]) # Check the type of the "Age" column (should be pandas.core.series.Series)

titanic["age"].max()
titanic["age"].shape # Number of elements in "age" column
```
**Explanation:**  
- Shows how to access, inspect, and analyze the "age" column.

---

### 4.7. **Filter Passengers Above Age 35**

```python
above_35 = titanic[titanic["age"] > 35]
above_35.head()

titanic["age"] > 35
```
**Explanation:**  
- Filters passengers older than 35.

---

### 4.8. **Find Missing Ages**

```python
titanic[titanic["age"].isna()]  # Display rows where "Age" is NaN (missing values)
```
**Explanation:**  
- Finds passengers with unknown age.

---

### 4.9. **Filter by Passenger Class**

```python
class_23 = titanic[titanic["pclass"].isin([2, 3])]  # Filter passengers in classes 2 and 3
print(class_23.head())
print(titanic['pclass'].unique())

class_23 = titanic[(titanic["pclass"] == 2) | (titanic["pclass"] == 3)]
print(titanic["pclass"].unique())
```
**Explanation:**  
- Filters passengers by class (2 or 3).

---

### 4.10. **Filter Rows Where Age Is Not NaN**

```python
age_no_na = titanic[titanic["age"].notna()]  # Filter rows where "Age" is not NaN
age_no_na.head()
age_no_na.shape

print("Passengers with known age:\n")
for age1 in age_no_na:
    print(age1) # Prints each row with known age
```
**Explanation:**  
- Keeps only rows with known age.
- `.shape` shows the number of rows and columns in the filtered DataFrame.
- Prints each row with known age.

---

### 4.11. **Names of Passengers Older Than 35**

```python
adults_name = titanic.loc[titanic["age"] > 35, "name"]   # .loc[] is used to access a group of rows and columns by labels or boolean arrays.
print("These are older than 35: \n")
for name in adults_name:
    print(name)
```
**Explanation:**  
- Selects and prints names of passengers older than 35.

---

### 4.12. **Selecting Subsets of Rows and Columns with iloc**

```python
# In this case, a subset of both rows and columns is made in one go and just using selection brackets [] is not sufficient.
# The loc/iloc operators are required in front of the selection brackets []. When using loc/iloc, the part
# before the comma is the rows you want, and the part after the comma is the columns you want to select.
# When using the column names, row labels or a condition expression, use the loc operator in front of the selection
# brackets []. For both the part before and after the comma, you can use a single label, a list of labels, a slice of labels,
# a conditional expression or a colon. Using a colon specifies you want to select all rows or columns.

# I’m interested in rows 10 till 25 and columns 3 to 5.
titanic.iloc[9:25 , 2:5]   # Selects rows 10-25 and columns 3-5 (by integer position, zero-based)

titanic.iloc[0:3, 3]       # Selects rows 0-2 and column 3 (by integer position)

titanic.head()             # Shows the first 5 rows
titanic.head().shape       # Shows the shape (rows, columns) of the first 5 rows
```
**Explanation:**  
- `.iloc` is used for integer-location based indexing.
- `titanic.iloc[9:25 , 2:5]` selects a block of rows and columns.
- `titanic.iloc[0:3, 3]` selects a single column for the first three rows.
- `.head().shape` shows the shape of the DataFrame returned by `.head()`.

---

## **Summary**

- This notebook covers Pandas basics, data cleaning, filtering, and analysis using the Titanic dataset.
- Each code line is explained for clarity.
- For further exploration, see the notebook file: `pandas.ipynb`.

---

## **License**

This project is for educational purposes.
- For further exploration, see the notebook file: `pandas.ipynb`.

---

## **License**

This project is for educational purposes.
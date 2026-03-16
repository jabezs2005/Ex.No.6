
# Experiment No. 6: How can you write a single function that automatically reads both .csv and .json files into a list of dictionaries?

## Aim: 
To write a single Python function that can automatically detect the file type (.csv or .json) and read its contents into a list of dictionaries.

## Explanation:
This experiment explores the concept of creating a versatile and reusable function that can handle different data formats, specifically .csv and .json. The core of this solution lies in using the file extension to determine the appropriate parsing method.

- For .csv files, the csv module's DictReader is ideal as it automatically maps rows to dictionaries based on the header.

- For .json files, the built-in json module's json.load() function can be used to parse the file content directly into a Python list of dictionaries.

- The function will check the file's extension and then call the correct parsing logic, providing a seamless user experience.

## AI Tools Required:
In this experiment, we'll use two different AI tools to generate the Python code and compare their outputs. This will allow us to analyze their strengths, weaknesses, and the quality of their generated solutions.

- AI Tool 1: Google Gemini

- AI Tool 2: ChatGPT

## Experiment:
### Prompt for AI Tools:

"Write a single Python function read_data_from_file(filepath) that can read both .csv and .json files. The function should return a list of dictionaries, where each dictionary represents a row (for .csv) or an object (for .json). The function must automatically detect the file type based on its extension."

### Analysis of AI Tool 1 (Google Gemini) Output:

Google Gemini generated a concise and correct function. It correctly used the os.path.splitext function to get the file extension, which is a robust way to handle file paths. The use of a try...except block to handle potential FileNotFoundError and ValueError (for invalid file format) is good practice. The code is readable and follows standard Python conventions.

### Generated Code:
```
Python

import csv
import json
import os

def read_data_from_file(filepath):
    """
    Reads data from a .csv or .json file and returns a list of dictionaries.

    Args:
        filepath (str): The path to the file.

    Returns:
        list: A list of dictionaries representing the data, or an empty list if an error occurs.
    """
    file_extension = os.path.splitext(filepath)[1].lower()

    if file_extension == '.csv':
        try:
            with open(filepath, 'r', newline='') as file:
                reader = csv.DictReader(file)
                return list(reader)
        except FileNotFoundError:
            print(f"Error: The file at {filepath} was not found.")
            return []
    elif file_extension == '.json':
        try:
            with open(filepath, 'r') as file:
                return json.load(file)
        except FileNotFoundError:
            print(f"Error: The file at {filepath} was not found.")
            return []
        except json.JSONDecodeError:
            print(f"Error: The file at {filepath} is not a valid JSON file.")
            return []
    else:
        print(f"Error: Unsupported file type. Only .csv and .json files are supported.")
        return []
```

### Example Usage:
### Create dummy files for testing
```
sample_csv_data = [
    {'name': 'Alice', 'age': '30'},
    {'name': 'Bob', 'age': '25'}
]
with open('data.csv', 'w', newline='') as csvfile:
    fieldnames = ['name', 'age']
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(sample_csv_data)

sample_json_data = [
    {'name': 'Charlie', 'age': 45},
    {'name': 'David', 'age': 50}
]
with open('data.json', 'w') as jsonfile:
    json.dump(sample_json_data, jsonfile)

# Test cases
csv_data = read_data_from_file('data.csv')
print("CSV Data:")
print(csv_data)

json_data = read_data_from_file('data.json')
print("\nJSON Data:")
print(json_data)

invalid_file_data = read_data_from_file('data.txt')
print("\nInvalid File Data:")
print(invalid_file_data)
```

### Analysis of AI Tool 2 (ChatGPT) Output:

ChatGPT provided a very similar solution, also using os.path.splitext and csv.DictReader. The code structure and logic are almost identical to Gemini's. It also included error handling, which is a crucial part of a production-ready function. Both tools correctly identified the need for a file extension check and a try...except block for robust error handling.

### Generated Code (ChatGPT):
```
Python

import csv
import json
import os

def read_data_from_file(file_path):
    """
    Reads data from a .csv or .json file and returns it as a list of dictionaries.

    Args:
        file_path (str): The path to the .csv or .json file.

    Returns:
        list: A list of dictionaries representing the data. Returns an empty list
              if the file is not found or is of an unsupported type.
    """
    file_extension = os.path.splitext(file_path)[1].lower()

    if file_extension == '.csv':
        try:
            with open(file_path, mode='r', encoding='utf-8') as infile:
                reader = csv.DictReader(infile)
                return [dict(row) for row in reader]
        except FileNotFoundError:
            print(f"Error: File not found at {file_path}")
            return []
        except Exception as e:
            print(f"An error occurred while reading the CSV file: {e}")
            return []
    elif file_extension == '.json':
        try:
            with open(file_path, mode='r', encoding='utf-8') as infile:
                return json.load(infile)
        except FileNotFoundError:
            print(f"Error: File not found at {file_path}")
            return []
        except json.JSONDecodeError:
            print(f"Error: Invalid JSON format in file at {file_path}")
            return []
        except Exception as e:
            print(f"An error occurred while reading the JSON file: {e}")
            return []
    else:
        print(f"Error: Unsupported file type. Please provide a .csv or .json file.")
        return []

# Example usage with dummy files
# (The dummy file creation logic is similar to Gemini's and is omitted for brevity)
# Test with a CSV file
print(read_data_from_file('data.csv'))

# Test with a JSON file
print(read_data_from_file('data.json'))
```
###  Data Science Learning Roadmap

<img width="250" height="200" alt="image" src="https://github.com/user-attachments/assets/97fd720d-bc1e-4b73-9462-0b50530dc23b" />

### Conclusion:
Both Google Gemini and ChatGPT successfully generated a robust and functional Python code that meets the requirements of the prompt. They both leveraged key Python libraries (os, csv, json) and implemented essential programming patterns like file extension checking, conditional logic, and error handling. The generated code is highly similar, demonstrating that both models have a strong understanding of this specific programming problem. The final code in the result section is a refined version combining the best practices from both outputs. The persona of the programmer is effectively captured through the clean and commented code that is ready for production use.
A single Python function read_data_from_file() was developed and implemented to automatically handle both .csv and .json file formats, reading their contents into a list of dictionaries. The function includes comprehensive error handling for file not found and invalid file format errors. The final code is presented below.

```
Python

import csv
import json
import os

def read_data_from_file(filepath):
    """
    Reads data from a .csv or .json file and returns a list of dictionaries.

    Args:
        filepath (str): The path to the file.

    Returns:
        list: A list of dictionaries representing the data, or an empty list if an error occurs.
    """
    file_extension = os.path.splitext(filepath)[1].lower()

    if file_extension == '.csv':
        try:
            with open(filepath, 'r', newline='', encoding='utf-8') as file:
                reader = csv.DictReader(file)
                return list(reader)
        except FileNotFoundError:
            print(f"Error: The file at {filepath} was not found.")
            return []
        except Exception as e:
            print(f"An error occurred while reading the CSV file: {e}")
            return []

    elif file_extension == '.json':
        try:
            with open(filepath, 'r', encoding='utf-8') as file:
                return json.load(file)
        except FileNotFoundError:
            print(f"Error: The file at {filepath} was not found.")
            return []
        except (json.JSONDecodeError, ValueError) as e:
            print(f"Error: The file at {filepath} is not a valid JSON file. {e}")
            return []
        except Exception as e:
            print(f"An error occurred while reading the JSON file: {e}")
            return []

    else:
        print(f"Error: Unsupported file type. Only .csv and .json files are supported.")
        return []

# --- Example Usage (for testing purposes) ---

# 1. Create dummy CSV and JSON files
try:
    with open("sample_data.csv", "w", newline='') as csvfile:
        fieldnames = ['id', 'name', 'city']
        writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
        writer.writeheader()
        writer.writerow({'id': 1, 'name': 'Alice', 'city': 'New York'})
        writer.writerow({'id': 2, 'name': 'Bob', 'city': 'London'})

    with open("sample_data.json", "w") as jsonfile:
        json.dump([
            {"id": 3, "name": "Charlie", "city": "Paris"},
            {"id": 4, "name": "Diana", "city": "Tokyo"}
        ], jsonfile, indent=4)
except Exception as e:
    print(f"Could not create dummy files: {e}")

# 2. Test the function with valid files
print("--- Reading CSV File ---")
csv_data = read_data_from_file("sample_data.csv")
print(csv_data)

print("\n--- Reading JSON File ---")
json_data = read_data_from_file("sample_data.json")
print(json_data)

# 3. Test the function with invalid files
print("\n--- Testing with a non-existent file ---")
read_data_from_file("non_existent_file.txt")

print("\n--- Testing with an unsupported file type ---")
with open("unsupported.txt", "w") as f:
    f.write("This is a text file.")
read_data_from_file("unsupported.txt")
os.remove("unsupported.txt") # Clean up

# 4. Clean up dummy files
try:
    os.remove("sample_data.csv")
    os.remove("sample_data.json")
except OSError:
    pass # Ignore if files don't exist
    
```

### Result:
The corresponding prompt was executed successfully, and the function worked correctly for both .csv and .json file inputs.

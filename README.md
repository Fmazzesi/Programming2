```markdown
# Python Package 2.0

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)

## Overview

Python Package 2.0 is a Python package designed to interact with the Zefix API for retrieving detailed information about companies, including acquisition details. The package provides flexible functions to obtain and process company data, supporting both simplified and detailed outputs, and can return data as pandas DataFrames for easier analysis.

## Features

- Retrieve detailed information about companies using their EHRAID.
- Flexible output options: list of dictionaries or pandas DataFrame.
- Translate company purposes and statuses into English.
- Simplified data retrieval options for quick lookups.

## Installation

To install the package, you can use pip:

```bash
pip install python-package-2.0
```

## Usage

### Example: Retrieving Acquirer Details

```python
from python_package_2.0 import check_acquirers

# Example of retrieving acquisition details for a company with EHRAID '110662'
ehraid = "110662"
acquired_details_df = check_acquirers(ehraid, df=True)
print(acquired_details_df)
```

### Function Descriptions

#### `check_acquirers(ehraid, simple=False, df=False)`

Retrieves information on companies acquired by the company with the given EHRAID.

**Parameters:**
- `ehraid` (str): Unique identifier of the company.
- `simple` (bool): If True, returns a simplified version of the data.
- `df` (bool): If True, returns the data as a pandas DataFrame.

**Returns:**
- List of dictionaries or a pandas DataFrame with acquisition details.

**Example Usage:**

```python
ehraid = "110662"
acquired_details_df = check_acquirers(ehraid, df=True)
print(acquired_details_df)
```

#### `get_acquisitions_data`

Retrieves acquisition data for a given EHRAID.

**Parameters:**
- `ehraid` (str): Unique identifier of the company.
- `df` (bool): If True, returns the data as a pandas DataFrame.

**Returns:**
- List of dictionaries or a pandas DataFrame with acquisition details.

**Example Usage:**

```python
from python_package_2.0 import get_acquisitions_data

# Example of retrieving acquisitions data
acquired_details_df = get_acquisitions_data('421132', df=True)
print(acquired_details_df)
```

## Contributing

Contributions are welcome! Please open an issue or submit a pull request with your improvements.

### How to Contribute

1. Fork the repository.
2. Create a new branch for your feature or bugfix.
3. Make your changes and commit them with clear messages.
4. Push your changes to your forked repository.
5. Open a pull request to the main repository.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For any questions or inquiries, please contact [Your Name] at [your.email@example.com].

---

### Detailed Explanation of Functions

#### `check_acquirers(ehraid, simple=False, df=False)`

This function is designed to retrieve detailed information on companies that have been acquired by the company identified by the provided EHRAID.

- **Parameters**:
  - `ehraid`: (str) The unique identifier of the company.
  - `simple`: (bool) If set to `True`, the function will return a simplified version of the data.
  - `df`: (bool) If set to `True`, the function will return the data as a pandas DataFrame.

- **Returns**:
  - A list of dictionaries or a pandas DataFrame containing details about the acquisitions.

- **Example**:
  ```python
  ehraid = "110662"
  acquired_details_df = check_acquirers(ehraid, df=True)
  print(acquired_details_df)
  ```

- **Internal Working**:
  - The function sends a POST request to the Zefix API with the provided `ehraid`.
  - It handles translation of specific fields such as `purpose` and `status` to English.
  - Constructs a list of dictionaries or a DataFrame based on the response.

#### `get_acquisitions_data(ehraid, df=False)`

This function serves as an example to showcase the use of `check_acquirers` function.

- **Parameters**:
  - `ehraid`: (str) The unique identifier of the company.
  - `df`: (bool) If set to `True`, the function will return the data as a pandas DataFrame.

- **Returns**:
  - A list of dictionaries or a pandas DataFrame containing details about the acquisitions.

- **Example**:
  ```python
  from python_package_2.0 import get_acquisitions_data

  # Example of retrieving acquisitions data
  acquired_details_df = get_acquisitions_data('421132', df=True)
  print(acquired_details_df)
  ```

## FAQ

### What is EHRAID?

EHRAID stands for the unique identifier assigned to each company in the Zefix database. It is used to uniquely identify companies for retrieving detailed information.

### How do I install dependencies?

You can install the required dependencies using pip. Ensure you have a `requirements.txt` file in your repository that lists all the necessary packages. Then run:

```bash
pip install -r requirements.txt
```

### How can I report an issue or suggest a feature?

Please use the GitHub issues tracker to report any issues or suggest new features. Make sure to follow the template provided for consistency and clarity.

---

# vuln-assessment
Recalculate vulnerabilities geared toward your org

# Vulnerability Severity Evaluation

This Python script evaluates the severity of a vulnerability based on the CVSS score, the number of endpoints affected, zero-day status, types of endpoints, and access type. The final severity score is normalized to a scale of 0-10.

## Function: `evaluate_vulnerability`

### Description

Evaluates the severity of a vulnerability based on the provided parameters.

### Parameters

- `cvss_score` (float): CVSS base score of the vulnerability.
- `num_endpoints` (int): Number of endpoints affected.
- `is_zero_day` (bool): Indicates if the vulnerability is a zero-day.
- `endpoint_types` (list): Types of endpoints affected (e.g., 'server', 'workstation').
- `access_type` (bool): Indicates if the user(s) have privileged access.

### Returns

- `float`: Adjusted severity score, normalized to a scale of 0-10.

### Implementation

```python
def evaluate_vulnerability(cvss_score, num_endpoints, is_zero_day, endpoint_types, access_type):
    """
    Evaluate the severity of a vulnerability based on CVSS score, number of endpoints,
    zero-day status, and types of endpoints.

    Args:
    cvss_score (float): CVSS base score of the vulnerability.
    num_endpoints (int): Number of endpoints affected.
    is_zero_day (bool): Indicates if the vulnerability is a zero-day.
    endpoint_types (list): Types of endpoints affected (e.g., 'server', 'workstation').
    access_type (bool): Indicates if the user(s) have privileged access.

    Returns:
    float: Adjusted severity score.
    """
    cvss_severity = (cvss_score / 4) * 10

    # Adjust severity based on the number of endpoints affected
    if num_endpoints >= 200:
        endpoint_severity = 10
    elif num_endpoints > 100:
        endpoint_severity = 6.67
    else:
        endpoint_severity = 3.33

    zero_day_severity = 10 if is_zero_day else 0

    endpoint_type_severity = 0
    if 'server' in endpoint_types:
        endpoint_type_severity += 10
    if 'workstation' in endpoint_types:
        endpoint_type_severity += 5

    access_severity = 10 if access_type else 0

    total_severity = (cvss_severity + endpoint_severity + zero_day_severity + endpoint_type_severity + access_severity) / 5
    return min(total_severity, 10)
```

## Function: `get_cvss_score`

### Description

Prompts the user to input a CVSS rating and returns the corresponding CVSS score.

### Returns

- `float`: CVSS score based on user input.

### Implementation

```python
def get_cvss_score():
    cvss_rating = input('Please enter the CVSS rating (critical, high, medium, low): ').strip().lower()
    match cvss_rating:
        case 'critical':
            return 4.0
        case 'high':
            return 3.0
        case 'medium':
            return 2.0
        case 'low':
            return 1.0
        case _:
            print("Invalid CVSS rating. Please enter 'critical', 'high', 'medium', or 'low'.")
            return get_cvss_score()  # Recursively ask for input again if invalid
```

## Usage

1. Run the script.
2. Provide the required inputs when prompted:
   - CVSS rating (critical, high, medium, low)
   - Number of endpoints
   - Zero-day status (yes/no)
   - Endpoint types (server, workstation)
   - Access type (privileged access: yes/no)
3. The script will output the adjusted severity score.

### Example

```python
# Get inputs from the user
cvss_score = get_cvss_score()
num_endpoints = int(input('Please enter the number of endpoints: ').strip())
is_zero_day = input('Is it a zero-day? (yes/no): ').strip().lower() in ['yes', 'y']
endpoint_types = input('Please enter the endpoint types separated by commas (server, workstation): ').strip().lower().split(',')
access_type = input('Do the user(s) have privileged access? (yes/no): ').strip().lower() in ['yes', 'y']

# Evaluate the adjusted severity
adjusted_severity = evaluate_vulnerability(cvss_score, num_endpoints, is_zero_day, endpoint_types, access_type)
print(f"Adjusted Severity Score: {adjusted_severity:.1f}")
```

This script provides a systematic approach to evaluating and normalizing the severity of vulnerabilities, ensuring a consistent assessment based on multiple factors.

# vuln-assessment
Recalculate vulnerabilities geared toward your org

# Vulnerability Severity Evaluation Tool

This Python script evaluates the severity of a cybersecurity vulnerability based on multiple factors including the CVSS score, the number of affected endpoints, whether the vulnerability is a zero-day, the types of affected endpoints, and whether the access is privileged.

## Features

- **CVSS Score Evaluation**: Converts the CVSS score to a severity rating.
- **Endpoint Analysis**: Assesses the impact based on the number of affected endpoints.
- **Zero-Day Flag**: Evaluates the increased risk of zero-day vulnerabilities.
- **Endpoint Type Consideration**: Differentiates between types of endpoints like servers and workstations.
- **Access Type Evaluation**: Considers whether the access is privileged to adjust the severity score.

## Usage

1. **Get CVSS Score**: Input the CVSS rating as 'critical', 'high', 'medium', or 'low'. The script will convert this into a numerical score.
2. **Input Number of Endpoints**: Enter the total number of affected endpoints.
3. **Zero-Day Status**: Specify if the vulnerability is a zero-day.
4. **Specify Endpoint Types**: Enter the affected endpoint types separated by commas (e.g., 'server, workstation').
5. **Privileged Access**: Indicate if the access is privileged.

The script will then calculate and print the adjusted severity score based on the inputs.

## Function Definitions

### `evaluate_vulnerability(cvss_score, num_endpoints, is_zero_day, endpoint_types, access_type)`

Evaluates the severity of a vulnerability.

#### Arguments:
- `cvss_score` (float): CVSS base score of the vulnerability.
- `num_endpoints` (int): Number of endpoints affected.
- `is_zero_day` (bool): Indicates if the vulnerability is a zero-day.
- `endpoint_types` (list): Types of endpoints affected (e.g., 'server', 'workstation').
- `access_type` (bool): Indicates if the user(s) have privileged access.

#### Returns:
- `float`: Adjusted severity score.

### `get_cvss_score()`

Prompts the user to enter a CVSS rating and returns the corresponding numerical score.

## Example Output

Adjusted Severity Score: 7.5


## Installation

No installation is required, just run the script in a Python environment capable of handling version 3.6 or newer.

## Contributing

Contributions to this project are welcome. Please fork the repository and submit a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

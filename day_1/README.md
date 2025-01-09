<<<<<<< HEAD

# Weather Dashboard Project

## Overview
The Weather Dashboard is a Python-based application that fetches real-time weather data for specified cities using the OpenWeather API and stores the data in an AWS S3 bucket. This project showcases skills in API integration, cloud storage management, and Python development.

## Features
- Fetches weather data for multiple cities.
- Retrieves information such as temperature, humidity, and weather conditions.
- Saves the weather data as JSON files in an AWS S3 bucket.
- Automatically creates the S3 bucket if it does not exist.

## Prerequisites
To run this project, ensure you have the following:
- Python 3.8 or higher installed.
- AWS account with programmatic access (Access Key ID and Secret Access Key).
- An API key from [OpenWeather](https://openweathermap.org/api).
- Required Python packages installed in a virtual environment.

## Installation and Setup

### 1. Clone the Repository
```bash
git clone <repository-url>
cd weather-dashboard-demo
```

### 2. Create and Activate a Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # For macOS/Linux
venv\Scripts\activate   # For Windows
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Set Up Environment Variables
Create a `.env` file in the project root with the following variables:
```env
OPENWEATHER_API_KEY=your_openweather_api_key
AWS_ACCESS_KEY_ID=your_aws_access_key_id
AWS_SECRET_ACCESS_KEY=your_aws_secret_access_key
AWS_BUCKET_NAME=your_s3_bucket_name
```

### 5. Run the Application
```bash
python weather-dashboard.py
```

## Project Structure
```
weather-dashboard-demo/
|
├── src/
│   ├── weather-dashboard.py  # Main application script
|
├── venv/                     # Virtual environment files
├── .env                      # Environment variables
├── requirements.txt          # List of Python dependencies
└── README.md                 # Project documentation
```

## How It Works
1. The application uses `requests` to fetch weather data from the OpenWeather API.
2. The `boto3` library interacts with AWS S3 to check for the existence of a bucket and store weather data files.
3. Weather data is saved in the `weather-data/` folder within the specified S3 bucket.

## Example Output
- Console Output:
```
Fetching weather for New York...
Temperature: 72°F
Feels like: 70°F
Humidity: 60%
Conditions: clear sky
Successfully saved data for New York to S3!
```

- S3 Bucket File Structure:
```
weather-data/
    New-York-20250107-103000.json
    Seattle-20250107-103500.json
    Philadelphia-20250107-104000.json
```

## Dependencies
- `boto3`: AWS SDK for Python.
- `requests`: To fetch weather data from the API.
- `python-dotenv`: For loading environment variables from a `.env` file.

## Troubleshooting
### Common Errors
1. **`ModuleNotFoundError: No module named 'boto3'`**
   - Ensure all dependencies are installed using `pip install -r requirements.txt`.

2. **`UnicodeDecodeError` during `load_dotenv()`**
   - Verify your `.env` file is encoded in UTF-8 without a BOM (Byte Order Mark).

3. **AWS Authentication Issues**
   - Confirm your AWS credentials are correct and have the required permissions.

## Future Enhancements
- Add a user-friendly web interface.
- Implement error logging with `logging` module.
- Schedule automatic weather updates using a task scheduler.
- Extend functionality to visualize weather data using charts.

## Author
ABIGAIL SYLVIE

## License
This project is licensed under the MIT License. For details, see the `LICENSE` file in the project repository.

=======
# weather-dashboard
The Weather Dashboard is a Python-based application that fetches real-time weather data for specified cities using the OpenWeather API and stores the data in an AWS S3 bucket. This project showcases skills in API integration, cloud storage management, and Python development.
>>>>>>> 316781fc0216debc4708d86d0540714d1549b75a

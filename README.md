# Boto3 Data Engineering Pipeline

A robust ETL (Extract, Transform, Load) pipeline that processes sales data using AWS S3, Apache Spark, and MySQL.

## Overview

This project implements a complete data engineering pipeline that:

1. Extracts sales data from AWS S3
2. Transforms it using Apache Spark for analysis
3. Loads processed data into MySQL and Parquet files
4. Generates valuable business insights on customer behavior and sales performance

## Features

- **Secure AWS Integration**
  - IAM Role authentication support
  - Environment-based configuration
  - S3 client with retry handling

- **Data Processing**
  - CSV validation and error handling
  - Parallel processing with Spark
  - Data mart creation (Customer & Sales)
  - Analytics calculation

- **Performance Insights**
  - Customer purchase pattern analysis
  - Sales team incentive calculation
  - Month-over-month growth tracking

- **Security & Best Practices**
  - No hardcoded credentials
  - Proper logging implementation
  - Automated cleanup of temporary files

## Architecture

```
┌─────────┐     ┌─────────────┐     ┌─────────────┐     ┌───────────┐
│ AWS S3  │────▶│ Data        │────▶│ Spark       │────▶│ MySQL DB  │
│ Bucket  │     │ Validation  │     │ Processing  │     │           │
└─────────┘     └─────────────┘     └─────────────┘     └───────────┘
                                          │
                                          ▼
                                    ┌─────────────┐
                                    │ Analytics & │
                                    │ Data Marts  │
                                    └─────────────┘
```

## Project Structure

- `/Boto3_DL/src/main/transformations/` - Core transformation logic
- `/Boto3_DL/src/main/utility/` - Reusable utility components
- `/Boto3_DL/resources/` - Configuration files
- `/Boto3_DL/resources/sql_scripts/` - SQL table definitions
- `/Boto3_DL/src/test/` - Test data generators

## Setup and Configuration

1. Clone the repository
```bash
git clone https://github.com/NikrrGit/Boto3_DataEngineering.git
cd Boto3_DataEngineering
```

2. Create and configure the `.env` file using the provided template
```bash
cp Boto3_DL/.env.template Boto3_DL/.env
chmod 600 Boto3_DL/.env  # Set proper permissions
```

3. Install required dependencies
```bash
pip install -r requirements.txt
```

4. Configure MySQL tables
```bash
mysql -u your_user -p < Boto3_DL/resources/sql_scripts/table_scripts.sql
```

## Usage

Run the main processing pipeline:
```bash
python Boto3_DL/src/main/transformations/jobs/main.py
```

Generate test data:
```bash
python Boto3_DL/src/test/generate_csv_data.py
```

## Security Recommendations

- Use IAM roles instead of access keys when possible
- Keep your `.env` file secure with restricted permissions (600)
- Rotate AWS credentials regularly
- Never commit credentials to version control

## Dependencies

- Python 3.9+
- AWS Boto3
- Apache Spark
- MySQL Connector
- Pandas/PyArrow
- Dotenv

## License

MIT

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

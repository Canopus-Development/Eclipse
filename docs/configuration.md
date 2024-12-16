
# Configuration Guide

## Overview

Eclipse can be configured using a configuration file, environment variables, or programmatically within your application.

---

## Configuration Methods

### Using a Configuration File

1. **Create** a configuration file (e.g., `config.yaml` or `config.json`).
2. **Specify** configuration parameters:

   ```yaml
   # config.yaml
   framework: flask
   database:
     type: sql
     connection_string: sqlite:///employees.db
   async_mode: false
   logging:
     level: INFO
   ```

3. **Load** the configuration file:

   ```python
   from eclipse import EmployeeManager
   import yaml

   with open('config.yaml', 'r') as f:
       config = yaml.safe_load(f)

   manager = EmployeeManager(**config)
   ```

### Using Environment Variables

Set environment variables for configuration parameters:

- `ECLIPSE_FRAMEWORK`
- `ECLIPSE_DATABASE_TYPE`
- `ECLIPSE_DATABASE_CONNECTION_STRING`
- `ECLIPSE_ASYNC_MODE`
- `ECLIPSE_LOGGING_LEVEL`

Example:

```bash
export ECLIPSE_FRAMEWORK=flask
export ECLIPSE_DATABASE_TYPE=sql
export ECLIPSE_DATABASE_CONNECTION_STRING=sqlite:///employees.db
```

The `EmployeeManager` will read these environment variables automatically.

### Programmatic Configuration

Pass configuration parameters directly when initializing:

```python
manager = EmployeeManager(
    framework='django',
    database={
        'type': 'mongodb',
        'uri': 'mongodb://localhost:27017/',
        'db_name': 'eclipse_db',
    },
    async_mode=True,
    logging={
        'level': 'DEBUG',
    }
)
```

---

## Configuration Parameters

- `framework` (str): Web framework to use (`'flask'`, `'django'`, `'fastapi'`).
- `database` (dict):
  - `type` (str): Database type (`'sql'`, `'mongodb'`, `'redis'`).
  - `connection_string` or `uri` (str): Connection URI.
  - Additional parameters depending on database type.
- `async_mode` (bool): Enable asynchronous operations.
- `logging` (dict):
  - `level` (str): Logging level (`'DEBUG'`, `'INFO'`, `'WARNING'`, `'ERROR'`, `'CRITICAL'`).
  - `handlers` (list): Custom logging handlers.

---

## Logging Configuration

Customize logging settings:

```python
import logging

logging_config = {
    'level': 'DEBUG',
    'handlers': [
        logging.StreamHandler(),
        logging.FileHandler('eclipse.log'),
    ],
}

manager = EmployeeManager(logging=logging_config)
```

---

## Example Configuration File

```json
{
  "framework": "fastapi",
  "database": {
    "type": "redis",
    "host": "localhost",
    "port": 6379
  },
  "async_mode": true,
  "logging": {
    "level": "INFO"
  }
}
```

---

## Best Practices

- **Separate** configuration from code for flexibility.
- **Secure** sensitive information like database credentials.
- **Document** your configuration settings for maintainability.

---

By following this guide, you can effectively configure Eclipse to suit your project's requirements.
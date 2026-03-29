---         
name: write-python-config-file                                                                                            
description: Write a Python config.py file. Use when creating or updating a config.py file for a project.
---

## Structure

- Use a single `Config` class to hold all constants. Do not use module-level variables for configuration values (except for setup like `load_dotenv()` and `BASE_DIR`).
- Use `UPPER_SNAKE_CASE` for all config values.
- Group related constants together with a blank line between each group.
- Use short `# Comments` above a group when the grouping isn't obvious from the variable names.

## Patterns

- Use `pathlib.Path` for all file/path values, with `joinpath()` for concatenation (not the `/` operator).
- Derive paths from `BASE_DIR = Path(__file__).resolve().parent` defined at the module level.
- Use `os.getenv()` for secrets and environment variables, with a default fallback.
- Use `dotenv` / `load_dotenv()` when `.env` files are needed, called at the module level before the class.
- Build compound values by referencing earlier class attributes (e.g. `FULL_URL = f"{BASE_URL}/path"`).

## Example

```python
import os
from pathlib import Path
from dotenv import load_dotenv


load_dotenv()

BASE_DIR = Path(__file__).resolve().parent


class Config:
    # Database
    DB_HOST = os.getenv("DB_HOST", "localhost")
    DB_PORT = 5432
    DB_NAME = "app_db"
    DB_URL = f"postgresql://{DB_HOST}:{DB_PORT}/{DB_NAME}"

    # API
    API_BASE_URL = "https://api.example.com/v1"
    API_KEY = os.getenv("API_KEY", "")
    API_TIMEOUT = 30

    # Logging
    LOG_DIR = BASE_DIR.joinpath("logs")
    LOG_PATH = LOG_DIR.joinpath("app.log")
    LOG_MAX_BYTES = 5 * 1024 * 1024  # 5 MB
    LOG_BACKUP_COUNT = 3
```

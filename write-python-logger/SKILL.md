---
name: setup-python-logger
description: Set up a Python file logger using RotatingFileHandler. Use when adding file logging to a new or existing Python script.
---

## Setup
 
- Define the logger at the module level, after imports and config.
- Create the log directory before setting up the handler using `mkdir(exist_ok=True)`.
- Use `pathlib.Path` with `joinpath()` for log paths, derived from `BASE_DIR = Path(__file__).resolve().parent`.
- Set the logger level to `logging.DEBUG`.
- Use ISO-style timestamp format: `"%Y-%m-%dT%H:%M:%S"`.
- Log format: `"[%(asctime)s] [%(levelname)s] %(message)s"`.
 
## Constants
 
The logging constants (`LOG_DIR`, `LOG_PATH`, `LOG_MAX_BYTES`, `LOG_BACKUP_COUNT`, `DIVIDER`) do not need to be in a `config.py`. For simple programs, they can sit at the top of the file. However, if the project already has a `config.py`, these
constants should be added there.
 
```python
LOG_DIR = BASE_DIR.joinpath("logs")
LOG_PATH = LOG_DIR.joinpath("app.log")
LOG_MAX_BYTES = 5 * 1024 * 1024  # 5 MB
LOG_BACKUP_COUNT = 3
DIVIDER = '='*80
```

## Example

```python
import logging
from logging.handlers import RotatingFileHandler

from config import Config

Config.LOG_DIR.mkdir(exist_ok=True)

logger = logging.getLogger("api")
logger.setLevel(logging.DEBUG)
handler = RotatingFileHandler(
  Config.LOG_PATH,
  maxBytes=Config.LOG_MAX_BYTES,
  backupCount=Config.LOG_BACKUP_COUNT,
)
formatter = logging.Formatter("[%(asctime)s] [%(levelname)s] %(message)s", "%Y-%m-%dT%H:%M:%S")

handler.setFormatter(formatter)
logger.addHandler(handler)
```

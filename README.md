# dygo

|     |     |
| --- | --- |
| Version | [![PyPI - Version](https://img.shields.io/pypi/v/dygo.svg)](https://pypi.org/project/dygo) [![PyPI - Python Version](https://img.shields.io/pypi/pyversions/dygo.svg)](https://pypi.org/project/dygo) |
| Project | ![GitHub License](https://img.shields.io/github/license/m-birke/dygo) ![PyPI - Status](https://img.shields.io/pypi/status/dygo) ![PyPI - Format](https://img.shields.io/pypi/format/dygo) ![PyPI - Implementation](https://img.shields.io/pypi/implementation/dygo) |
| CI | ![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/m-birke/dygo/static-code-check.yml) |
| Code | ![PyPI - Types](https://img.shields.io/pypi/types/dygo) [![Checked with mypy](https://www.mypy-lang.org/static/mypy_badge.svg)](https://mypy-lang.org/) [![Linting: Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/charliermarsh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff) [![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black) |

-----

Dynamic Gooey from config files

## Table of Contents

- [About](#about)
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)

## About

Dynamic Gooey (`dygo`) ...

1. Parses config files (json or yaml)
1. Extracts values which have to be defined by the user during runtime
1. Renders a GUI via [Gooey](https://github.com/chriskiehl/Gooey)
1. Let the user insert the values for the dynamic parameters
1. Inserts the received entries into the config
1. Returns the config

## Installation

```console
pip install dygo
```

## Usage

```python
from dygo import render

my_cfg = render("path/to/jsonORyaml")
```

The dynamic key needs to be inserted as a dict into the config file. The following two examples do the exact same.

- yaml

    ```yaml
    my_dynamic_param:
        dygo: 'room for a comment here'
        dest: 'param1'
    ```

- json

    ```json
    "my_dynamic_param": {"dygo": "dygo", "dest": "param1"},
    ```

The rendered GUI looks like this:

![example](img/example.png)

The dict will be replaced with the value received from the user. Assuming the user entered `abc` for `param1`, the dict afterwards looks like `{"my_dynamic_param": "abc"}`.

Currently the key `dygo` serves as a flag for Dynamic Gooey to detect dynamic parameters (the value is ignored). All other key-value pairs in the `dygo` dict are treated as args for `GooeyParser.add_argument` (see [Gooey](https://github.com/chriskiehl/Gooey) for further documentation). Most important is the `dest` arg whose value will be displayed as a name of the parameter for the user.

### Setting the Program Name & Description

```py
from dygo.config import set_program_metadata

set_program_metadata(program_name="My Program", program_description="It does what it does")
```

## License

`dygo` is distributed under the terms of the [MIT](https://spdx.org/licenses/MIT.html) license.

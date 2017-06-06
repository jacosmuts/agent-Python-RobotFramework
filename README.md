# ReportPortal RobotFramework agent

[![Build Status](https://travis-ci.org/reportportal/agent-Python-RobotFramework.svg?branch=master)](https://travis-ci.org/reportportal/agent-Python-RobotFramework)
[![PyPI](https://img.shields.io/pypi/v/robotframework-reportportal.svg?maxAge=2592000)](https://pypi.python.org/pypi/robotframework-reportportal)

Listener for RobotFramework to report results to ReportPortal

## Installation

First you need to install RobotFramework:

    pip install robotframework

The latest stable version of library is available on PyPI:

    pip install robotframework-reportportal

[reportportal-client](https://github.com/reportportal/client-Python) will be installed as a dependency

## Usage

For reporting results to ReportPortal you need to pass some variables to pybot run:

REQUIRED:
```
--listener robotframework_reportportal.listener
--variable RP_UUID:"your_user_uuid"
--variable RP_ENDPOINT:"your_reportportal_url"
--variable RP_LAUNCH:"launch_name"
--variable RP_PROJECT:"reportportal_project_name"
```
NOT REQUIRED:
```
--variable RP_LAUNCH_DOC:"some_documentation_for_launch"
    - Description for the launch
--variable RP_LAUNCH_TAGS:"RF Smoke"
    - Space-separated list of tags for the launch
--variable RP_LOG_BATCH_SIZE:"10"
    - Default value is "20", affects size of async batch log requests
```

Custom logger which supports attachments can be used in Python keywords.
Usage of this logger is similar to the standard robot.api.logger with addition
of an extra kwarg "attachment":

.. code-block:: python

    import subprocess
    from robotframework_reportportal import logger

    def log_free_memory():
        logger.debug("Collecting free memory statistics!")

        free_memory = subprocess.check_output("free -h".split())
        logger.debug(
            "Memory consumption report",
            attachment={
                "name": "free_memory.txt",
                "data": free_memory,
                "mime": "application/octet-stream",
            },
        )


## Copyright Notice
Licensed under the [GPLv3](https://www.gnu.org/licenses/quick-guide-gplv3.html)
license (see the LICENSE.txt file).

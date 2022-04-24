aw-client
=========

[![GitHub Actions badge](https://github.com/ActivityWatch/aw-client/workflows/Build/badge.svg)](https://github.com/ActivityWatch/aw-client/actions)
[![PyPI](https://img.shields.io/pypi/v/aw-client)](https://pypi.org/project/aw-client/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Typechecking: Mypy](http://www.mypy-lang.org/static/mypy_badge.svg)](http://mypy-lang.org/)

Client library for ActivityWatch in Python.

Please see [the documentation][docs] for usage, and take a look at `examples/`.

 - [Documentation][docs]
 - [API Reference][apiref]

[docs]: https://docs.activitywatch.net/en/latest/
[apiref]: https://docs.activitywatch.net/en/latest/api/python.html#aw-client

## How to install

Install from pip: `pip install aw-client`

Install the latest version directly from github without cloning: `pip install git+https://github.com/ActivityWatch/aw-client.git`

To install from a cloned version:

 - clone repo: `git clone https://github.com/ActivityWatch/aw-client.git`
 - cd into the directory: `cd aw-client`
 - run `poetry install` (will create a virtualenv, if none activated)
   - If you don't want to use poetry you can also use `pip install .`, but that might not get the exact version of the dependencies (due to not reading the `poetry.lock` file).

## Usage

For the CLI:

```
$ aw-client --help
Usage: aw-client [OPTIONS] COMMAND [ARGS]...

  CLI utility for aw-client to aid in interacting with the ActivityWatch
  server

Options:
  --host TEXT     Address of host
  --port INTEGER  Port to use
  -v, --verbose   Verbosity
  --testing       Set to use testing ports by default
  --help          Show this message and exit.

Commands:
  buckets    List all buckets
  canonical  Query 'canonical events' for a single host (filtered,...
  events     Query events from bucket with ID `bucket_id`
  heartbeat  Send a heartbeat to bucket with ID `bucket_id` with JSON `data`
  query      Run a query in file at `path` on the server
  report     Generate an activity report
```


## Debugging

* Run python with `LOG_LEVEL=debug` to get additional debugging output
* If invalid events have been queued for submission, you may need to delete the file-based queues generated by this library
* To use the development version of this library use `aw-client = {path = "../aw-client" }` in `pyproject.toml`

## Examples

The [`examples/`](examples/) directory contains a couple of example scripts, including:

 - [`time_spent_today.py`](examples/time_spent_today.py) - fetches all non-afk events and sums their duration to get the total active time for the day.
 - [`merge_buckets.py`](examples/merge_buckets.py) - merges two buckets with non-intersecting events by moving all events from one into the other.
 - [`redact_sensitive.py`](examples/redact_sensitive.py) - redact sensitive events.

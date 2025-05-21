# Python Pushwoosh Tools

## Requirements

- python 3.10 +

## Installation

```python
python3 -m venv venv # create python virtual environment
. venv/bin/activate # activate it
pip install -r requirements.txt # install dependencies
```

## Authorization

Currently, API token is required to authorize your requests.

Another authorization method using client-id, client-secret and account-id will be released [soon](https://wowwiki-archive.fandom.com/wiki/Soon).

There are three ways to provide API Token to the scripts: using `--token` argument, `.env` file and environment variable.

### `--token` argument
All scripts that require authorization accept `--token` argument.

Example:
```commandline
./export-segment --token XXXXX --app 00000-00000 'A("00000-00000")'
```

### `.env` file
Put the following content into the `.env` file to the project's directory:
```commandline
TOKEN=xxxxxxx
```

Then run script without `--token` argument:
```commandline
./export-segment --app 00000-00000 'A("00000-00000")'
./export-segment --app 00000-00000 'A("11111-11111")'
```

### Environment variable `TOKEN`
```commandline
TOKEN=xxxxxxx # setup token once
./export-segment --app 00000-00000 'A("00000-00000")' # then run several scripts
./export-segment --app 00000-00000 'A("11111-11111")'
```

## export-segment
Allows to export device data from Pushwoosh to CSV file.

Example:

```commandline
./export-segment --app 00000-00000 'A("00000-00000", [ios], [with_tokens]) * AT("00000-00000", "Last Application Open", daysago, gt, 3)' 
```

Supports any [seglang](https://docs.pushwoosh.com/platform-docs/api-reference/messages#sets) expression.

# process-segment

This tool iterates over the given CSV file and performs some action. Possible actions:
- registerDevice
- setTags
- unregisterDevice

Example:

```commandline
./process-segment -a registerDevice --app 00000-00000 export_segment_9A962-8ECD8_1666781735.csv
```


# ocds-tabulate

Transform OCDS data into a database.

This is a very preliminary version. [This document](https://docs.google.com/document/d/1ZK9crNn-9oB0ocdd5WkDLGw_qqGo3x5vZMoen8cLlyA/edit?usp=sharing) proposes what we are our future plans are.

## Installation

Clone this repository. Create a python virtual environment and enter it

```shell
virtualenv .ve -p python3

source .ve/bin/activate
```

Install the requirements

```shell
pip install -r requirements.txt
```

## Usage

To see the options.

```shell
python tabulate_ocds.py -h
```

It shows

```shell
usage: tabulate_ocds.py [-h] [--merge] [--drop] [--schema_url SCHEMA_URL]
                        database_url files [files ...]

Get some ocds data tabularized

positional arguments:
  database_url          sqlalchemy database url
  files                 json files to upload to db

optional arguments:
  -h, --help            show this help message and exit
  --merge               say if you want to ocds merge the files
  --drop                drop all current tables
  --schema_url SCHEMA_URL
                        schema file used
```

### Usage notes

For what to use as a database_url use the [sqlalchemy documentation](https://docs.sqlalchemy.org/en/rel_1_1/core/engines.html#database-urls). For example to use a sqlite file named ocds_data.db in the current directory use:

```shell
sqlite:///ocds_data.db
```

For the schema_url you need to point to the release_schema.json in the standard i.e.:

```shell
http://ocds.open-contracting.org/standard/r/1__0__2/release-schema.json
```

If not specified it will default to 1.0.2 verison.

The argument 'drop' will remove all the tables before the load. If this is not specified then the data load will append to the tables already existing.

## Example

```shell
python tabulate_ocds.py sqlite:///ocds_data.db my_ocds_package.json
```

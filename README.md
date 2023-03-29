# Auto Sqitch Script

## Installation

No installation is necessary.

You just need to copy the content of auto_squitch.sh inside a shell script at the root of your project. All example below are based on this name. Adapt it if you named it differently.

## Configuration

All configurations are at the beginning of the auto_squitch.sh

### Mandatory

You can change the directory where all migrations occur by changing the following variable :
```shell
# Folder where all migrations occurs
migration_folder=migrations
```

The additional script created by this one are specified by script_folder variable

```shell
# Folder where all scripts are located
script_folder=script
```

You can change the name of the versioning script created by default

```shell
# The script name for versioning
version_file_name=db_version
```

### Optional

You can force some information for script execution. It is recommended for the development environment. Comment the line to ignore is effect 

```shell
# Design the user of the sql server who own the database of the project
dbuser=admin_invoice
# Represent the database of the project
database=invoice
# The password of the sql user
dbpassword=invoice
```

## Usage

You need to run the script with the following command :

```shell
bash ./auto_sqitch.sh
```

It will prompt you several choices :

- init
  - Initialize sqitch with some setup and creating directory necessary for the project
- add
  - Add a new version to deploy with the command `sqitch add <filename> -n "comment`.
  - It will require two prompts : first one for the name of the file and second for commentary
  - The versioning script will be autocomplete each time this command run
- deploy OR revert OR verify
  - The last three can select all versioning available or the step you need to go

### Init

It will initialize a new project with sqitch :

The following variables are used during this process :

- `migration_folder`
- `script_folder`
- `version_file_name`
- `dbuser`
- `database`

The two following directories are create during the process, the name will be different if you change `migration_folder` and `script_folder` variables :

- Migrations, with his subdirectories "deploy", "revert", "verify"
  - This element is handled by sqitch itself with variables passed as arguments.
- Script, with the versioning script named by the `version_file_name`
  - This script handle this process.







# Auto Sqitch Script

## Installation

No installation is necessary except the sqitch tools.

For more information about sqitch, check the following link : [sqitch documentation](https://sqitch.org/)

You just need to copy the content of auto_squitch.sh inside a shell script at the root of your project. All example below are based on this name. Adapt it if you named it differently.

## Configuration

All configurations are at the beginning of the auto_squitch.sh between the comment block `Variable to modify`

### Specification

Check the table below :

| Environment | Variables to use                                                                                      | Notes                              |
|-------------|-------------------------------------------------------------------------------------------------------|------------------------------------|
| Production  | - migrations_folder<br/>- version_file<br/>- engine                                                   |                                    |
| Development | - migrations_folder<br/>- version_file_name<br/>- dbuser<br/>- database<br/>- dbpassword<br/>- engine | Add this file to `.gitignore` file |

### Mandatories variables

You can change the directory where all migrations occur by changing the following variable :
```shell
# Folder where all migrations occurs
migration_folder=migrations
```

You can change the name of the versioning script created by default

```shell
# The script name for versioning
version_file_name=db_version
```

You can specify the database engine you want to use

```shell
# The database engine used for the project
engine=pg
#engine=mysql
```

### Optionals variables

You can force some information for script execution. Comment the line to ignore is effect 

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

| Action | Script flag (Shortcut) | Description                                                                        |
|--------|------------------------|------------------------------------------------------------------------------------|
| init   | -i                     | Initialize sqitch with some setup and creating directory necessary for the project |
| update | -u                     | Update the existing file sqitch.plan if you clone a project which use sqitch       |
| add    | -a                     | Add a new version to deploy                                                        |
| deploy | -d                     | Deploy all or a specified version                                                  |
| revert | -r                     | Revert all or a specified version                                                  |
| verify | -v                     | Verify all or a specified version                                                  |
| help   | -h                     | Display a help message                                                             |


### Init

It will initialize a new project with sqitch. 

This command is to use when :
- you need to start a fresh sqitch project 
- you clone a repository which use sqitch

The following directory is created during the process, the name will be different if you change `migration_folder` variable :

- Migrations, with his subdirectories "deploy", "revert", "verify"
  - This element is handled by sqitch itself with variables passed as arguments.
  - inside there is a versioning script handle by this script. It will store every version you add.

### Update

It will update the file `sqitch.plan` with the last version added. It can be useful, if you already have this file on your project but ignored by git, to add newer version.

### Add

It will create a new version. All files are created following this pattern :

```shell
1.filename.sql
```

The number is added automatically, you just need to inform the filename during the prompt phase and add a comment.

### Deploy

It will deploy all versions at once or you can specify the version to go.

### Revert

It will revert all versions at once or you can specify the version to go.

### Verify

It will verify all versions at once or you can specify the version to go.







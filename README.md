# Database Code By Object Directories

This repository demonstrates how to organize database scripts in directories organized by database objects.

## Directory Structure
Here is the high-level overview of the directory structure. Note that there is a directory for each database (`database1`, `database2` and `database3`). These directories could also be renamed to match database names in case you are store scripts for MSSQL or other similar databases. 
```
.
├── README.md
├── liquibase.properties
└── sqlcode
    ├── rootchangelog.yaml
    ├── database1
    ├── database2
    └── database3
```

Following objects directories are used in this repo:
```
data
functions
index
materializedviews
packagebody
packages
procedures
database1changelog.yaml
tables
triggers
views
```

Here is the entire directory structure of this repo. Note that each database directory has its own changelog file (e.g., `database1changelog.yaml`). 

```.
├── liquibase.properties
└── sqlcode
    ├── rootchangelog.yaml
    ├── database1
    │   ├── database1changelog.yaml
    │   ├── data
    │   ├── functions
    │   ├── index
    │   ├── materializedviews
    │   ├── packagebody
    │   ├── packages
    │   ├── procedures
    │   ├── tables
    │   ├── triggers
    │   └── views
    ├── database2
    │   ├── database1changelog.yaml
    │   ├── data
    │   ├── functions
    │   ├── index
    │   ├── materializedviews
    │   ├── packagebody
    │   ├── packages
    │   ├── procedures
    │   ├── tables
    │   ├── triggers
    │   └── views
    └── database3
    │   ├── database1changelog.yaml
        ├── data
        ├── functions
        ├── index
        ├── materializedviews
        ├── packagebody
        ├── packages
        ├── procedures
        ├── tables
        ├── triggers
        └── views
```

## Changelog files
Note that there is a [rootchangelog.yaml](sqlcode/rootchangelog.yaml) which serves as the entry point changelog for Liquibase (as specified in [liquibase.properties](liquibase.properties) file). This file points to databaseXchangelog.yaml files:
```yaml
- include:
    file: database1/database1changelog.yaml
    relativeToChangelogFile: true
- include:
    file: database2/database2changelog.yaml
    relativeToChangelogFile: true
- include:
    file: database3/database3changelog.yaml
    relativeToChangelogFile: true
```

Each databaseXchangelog.yaml file points to a changelog.yaml file in each object directory:
```yaml
- include:
    file: sequence/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: tables/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: index/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: functions/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: views/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: procedures/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: packages/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: packagebody/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: triggers/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: data/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: materializedviews/changelog.yaml
    relativeToChangelogFile: true
```


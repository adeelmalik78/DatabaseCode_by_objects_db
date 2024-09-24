# Database Code By Object Directories

This repository demonstrates how to organize database scripts in directories organized by database objects.

## Directory Structure
Here is the high-level overview of the directory structure. Note that there is a directory for each schema (`schema1`, `schema2` and `schema3`). These directories could also be renamed to match database names in case you are store scripts for MSSQL or other similar databases. 
```
.
├── README.md
├── liquibase.properties
└── sqlcode
    ├── rootchangelog.yaml
    ├── schema1
    ├── schema2
    └── schema3
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
schema1changelog.yaml
tables
triggers
views
```

Here is the entire directory structure of this repo. Note that each schema directory has its own changelog file (e.g., `schema1changelog.yaml`). 

```.
├── liquibase.properties
└── sqlcode
    ├── rootchangelog.yaml
    ├── schema1
    │   ├── schema1changelog.yaml
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
    ├── schema2
    │   ├── schema1changelog.yaml
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
    └── schema3
    │   ├── schema1changelog.yaml
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
Note that there is a [rootchangelog.yaml](sqlcode/rootchangelog.yaml) which serves as the entry point changelog for Liquibase (as specified in [liquibase.properties](liquibase.properties) file). This file points to schemaXchangelog.yaml files:
```yaml
- include:
    file: schema1/schema1changelog.yaml
    relativeToChangelogFile: true
- include:
    file: schema2/schema2changelog.yaml
    relativeToChangelogFile: true
- include:
    file: schema3/schema3changelog.yaml
    relativeToChangelogFile: true
```

Each schemaXchangelog.yaml file points to a changelog.yaml file in each object directory:
```yaml
- include:
    file: tables/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: index/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: views/changelog.yaml
    relativeToChangelogFile: true
- include:
    file: functions/changelog.yaml
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


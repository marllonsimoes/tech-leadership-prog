# Data Storage

## Decision table

The decision was based on pros/cons tablecomparing free oss vs. paid solution based on support, features, needs and team knowledge.

![Database comparison](https://content.altexsoft.com/media/2019/06/database-management-systems-comparison.png "Database comparison table")

## Points taken into consideration

- Flexibility
- dev environment with same capabilities as production
- no vendor lockin
- migration to a different platform
- community
- pontual paid support (to reduce costs)
- other components that can be part of the ecosystem
- previous knowledge/experience

## Application requirements

* CRUD operations
* Filtering
* Search
* Sorting
* Aggregation by specified field value

PgSQL offers indexes, partitions and other techniques to segregate the data based on any need users may have.

* Data storage for REST service should provide support multi-tenant content storage.
* Data Storage should scale so that:
  * up to 100 000 000 of records are stored
  * CRUD operations and typical search queries should execute within 1 second

PgSQL offers several different tools to perform backups, dumps and copy of data to a file or  another database
* Data storage should support automated data backup every 30 days.

PgSQL have integration with OS events and can be monitored using available market tools such as prometheus, zabbix, newrelic and others
* Data storage should support detailed logging for troubleshooting.

Despite the fact this requirement is not yet as clear, PgSQL can be depoyed and replicated manually to as many instances as required. When it comes to Distributed database (if this would be the way to go with this requirement), cockroachdb might be the optimal option for such case. It can be replicated between regions, zones, bare-metal or cloud.
* The infrastructure should support two European regions: east and west.

## Conclusion
When it comes to team knowledge, pgsql, mysql, mongodb are in the top of the list.
Given the requirements, budget, extensibility, possibility of migration to a different platform and the involvement of other teams, we chose postgresql as a database storage because of:

- dev environment can be very similar to production, given a sample of production data
- no vendor lock-in as it doesn´t require any proprietary technology or language or plataform to execute maintenance. Scripts and data can be migrated to any other provider that supports market standarts.
- community is big enough and very active
- offers support plans and there are plenty of evangelists here and there that can also offer support
- it is the core of several different rdbms' such as cockroach db, yugabyteDB and others, that provide distributed scalability.
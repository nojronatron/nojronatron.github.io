# Deploying Node.js Web App with Mongo DB to Azure

## Mongo DB Stuff

[Mongodb v4.2 reference page](https://www.mongodb.com/docs/v4.2/reference/configuration-options/)

Config File: `/etc/mongod.conf`

File format: 'yaml' so no tabs just spaces (extension is conf though).

Tell mongo to use a specific configuration: `mogod|mogos --config /etc/mongod.conf`

Config file shows where logging is done. Mine is currently `/var/log/mongodb/mongod.log`

Config file shows where db files are stored. Mine is currently: `/var/lib/mongodb`

'systemLog.verbosity' is an integer, default 0. Can be increased up to 5 (debug).

## References

[MongoDB Configuration Options](https://docs.mongodb.org/manual/reference/configuraiton-options)

## Footer

Return to [conted index](./conted-index.html)

Return to [ROOT README](../README.html)

# c8y-analytics
go-c8y-cli extension for Streaming Analytics.

The extension currently supports

**Analytics Builder Models**

* List all Analytics Builder models on a tenant
* Getting / Updating / Deleting individual Analytics Builder models
* Changing the state of an Analytics Builder model (active, inactive)
* Changing the mode of an Analytics Builder model (DRAFT, TEST, SIMULATION, PRODUCTION)
* Listing / Updating / Deleting of all instance of an Analytics Builder Template model

**EPL Apps**

* List all EPL Apps on a tenant
* Getting / Updating / Deleting individual EPL Apps
* Changing the state of an EPL App (active, inactive)

**Streaming Analytics Management**

* Restart Apama microservice
* Get health and versioning information of the Apama microservice
* Retrieve diagnostics overview and full view
* Retrieve microservice logs / events / alarms
* Configure the Apama microservice via tenant options

**Extension Management**

* List all installed Analytics extensions
* Get details on an individual Analytics extension
* Delete Analytics extensions
* Download & upload Analytics extensions

## Installation

The extension can be installed using the following command.

```sh
c8y extension install Cumulocity-IoT/c8y-analytics
``` 

## Usage examples

### Analytics Builder Models

List all Analytics Builder models:
```
c8y analytics ab list
```

Download a specific Analytics Builder model:
```
c8y analytics ab get --id 5379731810 --outputFileRaw iir.json
```

Upload a new Analytics Builder model:
```
c8y analytics ab create --name iir2 --template iir.json
```

Update the state of an Analytics Builder model:
```
c8y analytics ab update --id 1579830237 --state ACTIVE
```

Delete an Analytics Builder model:
```
c8y analytics ab delete --id 1579830237
```

### EPL Apps

EPL Apps support the same commands, like Analytics Builder models. For example, to list all EPL Apps:

List all EPL Apps:
```
c8y analytics epl list --includeAll
```

**Note:** The list of Analytics Builder models always includes all models, whereas the list EPL Apps uses pagination.

### Analytics Builder Template Models
Template models are a way to parameterize models and then create multiple instances with different values for these parameters.

List all instances of a template model:
```
c8y analytics instances list --id 2579780855
```

Update an instance of a template model:
```
c8y analytics instances update --id 2579780855 --instanceId 9579789317 --mode PRODUCTION
```
**Note:** This command is mostly useful to apply state and mode changes. While changes to parameter values are possible it requires to provide all parameters via the --data flag.

Delete an instance of a template model:
```
c8y analytics instances delete --id 2579780855 --instanceId 9579789317
```

### Management
These commands provide control over the Apama microservice that provides the Streaming Analytics capabilities of Cumulocity.

Restart the Apama microservice (e.g. after deploying custom blocks):
```
c8y analytics management restart
```

Get full diagnostics of the Apama microservice (the command uses the file name provided by the Apama microservice):
```
c8y analytics management diagnosticsEnhanced --outputFileRaw "{filename}" > /dev/null
```

### Apama microservice status
These commands give detailed status information on the Apama microservice.

Retrieve the logs of the Apama microservice:
```
c8y analytics status logs
```

Retrieve the deployment and status change events of the Apama microservice:
```
c8y analytics status events
```

Retrieve all critical alarms related to the Apama microservice:
```
c8y analytics status alarms --severity CRITICA
```

### Configuration

Configure the delay used for reordering and ignoring data. For details refer to the documentation on [Input blocks and event timing](https://cumulocity.com/docs/streaming-analytics/analytics-builder/#input-blocks-and-event-timing).
```
c8y analytics configuration update --key analytics.builder/timedelay_secs --value 180
```

In addition, commands exist to configure the number of client the Apama microservice uses to interact with Cumulocity and the number of worker threads Analytics Builder uses.

### Analytics Extensions

Analytics extensions are used to deploy custom blocks for Analytics Builder and other customizations into the Apama microservice. They can be built using the [Apama Analytics Builder Block SDK](https://github.com/Cumulocity-IoT/apama-analytics-builder-block-sdk).

List all Analytics extensions:
```
c8y analytics extensions list --includeAll
```

Get the details of an individual Analytics extension by id:
```
c8y analytics extensions get --id 1779829394
```

Delete an Analytics extension:
```
c8y analytics extensions delete --id 1779829394
```

Download an Analytics extension:
```
c8y analytics extensions download --id 1179099345 --outputFileRaw MyBlocks.zip  > /dev/null
```


Upload an Analytics extension built with the Block SDK:
```
c8y analytics extensions upload --file MyBlocks.zip --verbose --name MyBlocks --template '{pas_extension:$.name}'
```




## Licensing

This project is licensed under the Apache 2.0 license - see <https://www.apache.org/licenses/LICENSE-2.0>

______________________

These tools are provided as-is and without warranty or support. They do not constitute part of the Cumulocity product suite. Users are free to use, fork and modify them, subject to the license agreement. While Cumulocity GmbH welcomes contributions, we cannot guarantee to include every contribution in the master project.

______________________

You can find additional information in the [Cumulocity Community](https://techcommunity.cumulocity.com/).
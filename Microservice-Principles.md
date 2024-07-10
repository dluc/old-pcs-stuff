These principles will stay consistent across all microservices (both Java and .NET).  

* Project structure for the microservices needs to stay consistent (Service, Service.Test, WebService, WebService.Test, Scripts, etc.)
* Travis integration needs to be used for CI.
* Build scripts need maintained & tested before each PR is pushed.
* All IoT Hub interaction should solely use the SDKs – we should never go around the SDK by using the REST API directly.  Instead we’ll work with the SDK team to improve the SDKs.
* Technology choices inside microservices need to use the tech choice criteria defined here:  https://github.com/Azure/azure-iot-pcs-team/wiki/Dependencies.  
* Java and .NET REST API surface need to be the same. Clients of the web service will be able to expect an identical API surface between the two including request and response payloads.  
  * Note in most cases the SDK models cannot be exposed directly, because the .NET SDK models are often different from Java SDK models; e.g. the IoTHub Java and dotNet SDK models don't match.
* We standardize on using CamelCasing, not pascalCasing for all property names in all JSON payloads for getters and setters.
* Java and .NET need to have tech dependencies that resonate with the Java and .NET audiences respectively; e.g. using Azure Table Storage might resonate with a .NET developer while it won’t for a Java developer (Cassandra might be a better fit).
* Services/Applications should always wrap external resource models, e.g. models coming from external libraries like SDKs. This reduces the risk of leaking implementation details, and helps maintaining cross-language API specifications. SDKs sometimes introduce new features or breaking changes. The public facing code needs to be insulated from these changes through a thin wrapper.
* Services should be designed to allow swapping internal dependencies, in other words reducing end-to-end coupling. Examples: 
  * Given a service that requires storage (think UI Config microservice), it should be simple to move from Cassandra, to DocDB, to Mysql, etc. without changing the API specification, and without major re-architecture. 
  * Azure IoT Hub will continue to provide new features, and IoT Hub Manager integration through the SDK will grow in complexity. IoT Hub Manager API should shield client services as much as possible from this complexity. For example, once we integrate PCS with Edge or DPS, the public API of the HubManager microservice will stay the same, but much more will happen internally.
* Integration points between (micro)services should be covered by integration tests, to discover breaking changes quickly, before merging changes into the main code repository. Integration tests should not be "*fixed*" changing the test code, but rather, understanding the design change impact on other microservices. We assume/hope that customers will build proprietary applications around PCS components, so it's important to maintain a stable API contract. When needed we'll use API versioning, however we should not have to maintain too many API versions, and we should not ask customers to upgrade to a new version too often.


# Update 7/23/2017

All microservices and components should follow the same naming conventions:

1. Microservices offering a set of features usable outside the context of a Solution, should not use a "pcs" prefix. Examples: IoT Hub Manager, Device Telemetry, Device Simulation and Stream Analytics.
2. Microservices specific to IoT PCS, should use a "pcs" prefix. Examples: CLI, UI Config, Web UI, Storage adapter.
3. Environment variables:
   1. Should have a `PCS_` prefix
   1. Should merge the service name into one word, without `_`, removing the `pcs` prefix if present.
   1. Should use one word and the same abbreviations for common concepts, examples:
      1. Connection strings: `CONNSTRING` is ok, we should not use `CONN_STRING` or `CONNECTION_STRING`
      1. IoT Hub: `IOTHUB` is ok, we should not use `IOT_HUB`
   1. Some examples:
      1. `PCS_STORAGEADAPTER_WEBSERVICE_PORT` ==> OK
      1. `PCS_UICONFIG_WEBSERVICE_PORT` ==> OK
      1. `PCS_DEVICESIMULATION_WEBSERVICE_PORT` ==> OK
      1. `PCS_IOTHUBMANAGER_WEBSERVICE_URL` ==> OK
      1. `PCS_IOTHUBMANAGER_WEBSERVICE_PORT` ==> OK
      1. `PCS_STREAMANALYTICS_WEBSERVICE_PORT` ==> OK
      1. `PCS_DEVICETELEMETRY_WEBSERVICE_PORT` ==> **TO BE FIXED** (curr. `PCS_DEVICE_TELEMETRY_WEBSERVICE_PORT`)
      1. `PCS_IOTHUB_CONNSTRING` ==> **TO BE FIXED** (curr. `PCS_IOTHUB_CONN_STRING`)

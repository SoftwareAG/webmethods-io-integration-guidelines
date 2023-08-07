# 8 Hybrid Integration

Hybrid integration can be used to connect a self-hosted execution environment, allowing webMethods Integration Server FlowServices to be executed on that particular environment.

Self-hosted FlowService(s) that require Hybrid Integration can be developed using Software AG's Designer tool. The service(s) metadata can then be published to the cloud to auto create connector(s) that allows them to be invoked from webMethods.io Integration.  This is a very powerful function for invoking existing self-hosted integrations or running what can be very complex integrations close to a source system (e.g. a self-hosted database, or an SAP ERP).

Please be aware that routing to a hybrid integration is subject to latency and bandwidth restrictions from the cloud to wherever the hybrid end point is located.

To minimize this, it's recommended to avoid making lots of repeated calls to a hybrid endpoint by creating a wrapper service in the self-hosted execution environment that collects a call from the cloud, makes multiple calls back to the source system, and then returns results to the cloud once ready.

Please note also - hybrid integration calls have a maximum size limit of 50MB.

To send hybrid messages efficiently, please consider compressing your payload instead of sending multi-byte XML as text. This allows faster (because smaller) data transfer as well as sending larger amounts of data.

It's also recommended to check the size of the compressed object before sending to avoid trying to send a message larger than the limits.

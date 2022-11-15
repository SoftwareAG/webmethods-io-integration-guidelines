# 8 Hybrid Integration

Hybrid integration can be used to connect an on-premise/self-hosted execution environment, allowing FlowSerivces to be executed on that particular environment.

FlowServices requiring Hybrid Integration can be developed using Software AG's designer tool, and then published ot the cloud to auto create a connector that allows this to be invoked.  This is a very powerful function for invoke existing integrations or running what can be very complex integrations close to a source system (e.g. a self-hosted database, or an SAP ERP).

Please be aware routing to a hybrid integration is subject to latency and bandwidth restrictions from the cloud to wherever the hybrid end point is located.

To minimize this, it's recommended to avoid making lots of repeated calls to a hybrid endpoint by creating a wrapper service in the self-hosted exection environment that collects a call from the cloud, makes multiple calls back to the source system, and then returns back to the cloud once ready.

Please note also - hybrid integration calls have a maximum size limit of 50MB.

Streaming Application Logs to Log Management Services 
----------------------------------------------------------------

Cloud Foundry aggregates logs for all instances of your applications as well as 
for requests made to your applications through internal components of Cloud Foundry. 

For example, when the Cloud Foundry Router forwards a request to an application, 
the Router records that event in the log stream for that app. 

Run the following command to access the log stream for an app in the terminal:

$ cf logs YOUR-APP-NAME


If we want to persist more than the limited amount of logging information that Cloud
Foundry can buffer, drain these logs to a log management service.

Using Services from the Cloud Foundry Marketplace
----------------------------------------------------------

$ cf create-service SERVICE PLAN SERVICE-INSTANCE
$ cf bind-service YOUR-APP YOUR-LOG-STORE


Using Services Not Available in Your Marketplace
-------------------------------------------------------

If a compatible log management service is not available in your Cloud Foundry 
marketplace, you can use user-provided service instances to stream application
logs to a service of your choice.

You can install and use the CF Drain CLI Plugin to create and manage user-provided
syslog drains from the CF command-line interface (cf CLI).


Step 1: Configure the Log Management Service
-----------------------------------------------------
Complete the following steps to set up a communication channel between the log 
management service and your Cloud Foundry deployment:

>Obtain the external IP addresses that your Cloud Foundry administrator assigns to 
outbound traffic.

> Provide these IP addresses to the log management service. The specific steps to 
configure a third-party log management service depend on the service.

> Whitelist these IP addresses to ensure unrestricted log routing to your log 
management service.

> Record the syslog URL provided by the third-party service. Third-party services 
typically provide a syslog URL to use as an endpoint for incoming log data. 

You use this syslog URL in Step 2: Create a User-provided Service Instance. 

Cloud Foundry uses the syslog URL to route messages to the service. The syslog URL
has a scheme of syslog, syslog-tls, or https, and can include a port number. For example:
syslog://logs.example.com:1234


Step 2: Create and Bind a User-Provided Service Instance

You can create a syslog drain service and bind apps to it using either generic 
Cloud Foundry Command Line Interface (cf CLI) commands, or drain-specific 
commands enabled by the CF Drain plugin for the cf CLI.

cf create-user-provided-service articulate-log-drain -l syslog://{{syslog_drain_url}}
(OR)
cf create-drain APP-NAME DRAIN-NAME SYSLOG-DRAIN-URL


Step 3: Verify Logs Are Draining

To verify that logs are draining correctly to a third-party log management service:

> Take actions that produce log messages, such as making requests of your app.
> Compare the logs displayed in the CLI against those displayed by the log management service.








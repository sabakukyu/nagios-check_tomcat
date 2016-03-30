# **check_tomcat (plugin for Nagios)**

The *check_tomcat* script is designed to monitor *Apache Tomcat* through *JMX Proxy Servlet* in combination with *check_by_ssh* plugin. The first step is to ensure that the central *Nagios* server is able to connect to the remote host via *SSH* in a manner that does not require a password. The second step is to ensure that the user executing *check_tomcat* plugin has read permissions on *"${CATALINA_BASE}/conf/tomcat-users.xml"* file. Finally, to access *JMX proxy interface* requires at least one user with the role *manager-jmx* and whose password is not encrypted.

The *check_tomcat* script has four different check types and each monitors the following metrics:

  * **apps**: *activeSessions*
  * **memory**: *HeapMemoryUsage*, *NonHeapMemoryUsage*
  * **pools**: *numActive*
  * **threads**: *currentThreadsBusy*

Check types **memory** and **threads** return *performance data* in their output (others return *'null'*).

This plugin has been tested with *Apache Tomcat* **6.x** and **7.x** (forward compatibility not guaranteed).

## Requirements

The *check_tomcat* script is programmed for *bash* shell and requires one utility to work properly:

  * *check_by_ssh* (plugin for Nagios, discussed above)

All other required commands (such as: *curl*, *grep*, *sed*, *...*) are very common and are not listed.

## Usage

```sh
$ ./check_tomcat --help
Usage: ./check_tomcat [-h] [-v] -n instance_name -k service_check [-w service_warning] [-c service_critical]

  -c, --critical
    Specifies the 'critical' level check. If the service check is 'apps' the value is treated as
    a literal number, in any other case is treated as a percent. Default value is 90.

  -h, --help
    Shows this help message.

  -k, --check
    Specifies the service check. Accepted values are: apps, memory, pools and threads.

  -n, --name
    Specifies the instance name.

  -v, --verbose
    Enable verbose logging of what check_tomcat is doing.

  -w, --warning
    Specifies the 'warning' level check. If the service check is 'apps' the value is treated as
    a literal number, in any other case is treated as a percent. Default value is 75.

Example: ./check_tomcat -n tomcat -k memory -w 75 -c 90

This example will report CRITICAL if the current JVM heap/nonheap usage exceeds 90% or WARNING
if the heap/nonheap usage exceeds 75%.
```

## To-Do

  * Add code comments
  * Better error handling

## 

Joaquín José García Cañas (https://github.com/sabakukyu)

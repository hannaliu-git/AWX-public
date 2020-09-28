### Add / Remove Netflow configuriation

The goal for this playbook is to add/remove netflow configuration on Cisco IOS with the following attributes. 
-	Set/Reset netflow timeouts
-	Create/Remove a flow exporter
-	Create/Remove a flow monitor
-	Assign/Remove flow monitor to/from selected interfaces


### Platforms
Cisco IOS

### Future Support
Cisco Nexus

### Prerequisite
The flow exporter originating interface, eg. Loopback interface, needs to be configured prior to adding netflow configuration. 

#### How to use:
The only user input required will be to update the netflow dictionary to reflect what you want to configure on the devices. 
Provide inputs in the file called 'all.yml'. Update the values for add_Netflow and remove_Netflow depends on whether you want to add or remove the netflow configuration. And then update the rest of the values in the dictionary. 

Then run the playbook add_remove_netflow.yml. 

#### Input file format

    ---
    # IOS
    # Add netflow configuration
    # add_Netflow: true
    # remove_Netflow: false
    # Mandatory Arg: all fields

    # IOS
    # Remove netflow configuration
    # add_Netflow: false
    # remove_Netflow: true
    # Mandatory Arg: (timeout_active, flow_exporter_name, flow_monitor_name, interfaces)

    ## Arguments option ##
    # add_Netflow: 'true' or 'false'
    # remove_Netflow: 'false' or 'true'
    # timeout_active:  [1-60,  Active netflow cache timeout in minutes, eg. 1]
    # flow_exporter_name: [Flow exporter name, eg. MyNetflow]
    # description: [Flow exporter description, eg. export to netflow]
    # flow_exporter_destination: [Destination hostname or IPv4 address or IPv6 address, eg. 5.5.5.5]
    # source: [Originating interface, eg. loopback0]
    # transport_protocol: [Transport protocol and port number, eg. udp 9995]
    # export_protocol: [Export protocol version, eg. netflow-v5]
    # flow_monitor_name: [Flow Monitor name, eg. MyMonitor]
    # cache_timeout_active: [1-604800, Active flow monitor cache timeout in seconds, eg. 60]
    # record: [Specify flow record to use to define cache, eg. netflow-original]
    # interfaces: [Selected interfaces which are assigned flow monitor, eg. f0/0]

    ## eg. for adding netflow config ##
        ---

        Netflow:
        # for adding netflow, provide all values below
        add_Netflow: true
        # for removing netflow, only need to provide values for timeout_active, flow_exporter_name, flow_monitor_name and interfaces
        remove_Netflow: false

        # timeouts value
        timeout_active: 1

        # flow exporter values
        flow_exporter_name: MyNetflow
        description: export to netflow
        flow_exporter_destination: 5.5.5.5
        source: loopback0
        transport_protocol: udp 9995
        export_protocol: netflow-v5

        # flow monitor values
        flow_monitor_name: MyMonitor
        cache_timeout_active: 60
        record: netflow-original

        # interfaces with flow monitor
        interfaces:
            - f0/0
            - e1/0



    ## eg. for removing netflow config ##
        ---
        
        Netflow:
        # for adding netflow, provide all values below
        add_Netflow: false
        # for removing netflow, only need to provide values for timeout_active, flow_exporter_name, flow_monitor_name and interfaces
        remove_Netflow: true

        # timeouts value
        timeout_active: 1

        # flow exporter values
        flow_exporter_name: MyNetflow
        description: 
        flow_exporter_destination: 
        source: 
        transport_protocol: 
        export_protocol:

        # flow monitor values
        flow_monitor_name: MyMonitor
        cache_timeout_active: 
        record: 

        # interfaces with flow monitor
        interfaces:
            - f0/0
            - e1/0


### Return values
On completion, the playbook will output a report detailing the pre and post Netflow configuration for each device that it executed for.
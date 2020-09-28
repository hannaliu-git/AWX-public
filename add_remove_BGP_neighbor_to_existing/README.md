### Add / Remove BGP neighbor to existing BGP process

The goal for this playbook is to add/remove BGP neighbor to existing BGP process on Cisco IOS. 

### Platforms
Cisco IOS

### Future Support
Cisco Nexus

### Prerequisite
If BGP update source, inbound route map and outbound route map need to be configured for the new bgp neighbor, the update source, inbound route map and outbound route map need to be configured respectively prior to the new BGP neighbor configuration.

If send-community needs to be configured, the prefixes and route map need to be configured prior to the new BGP neighbor configuration in order to make it work. 

### Limitation
This playbook supports the BGP neighbor configuration for setting neighbor, remote_as, description, ebgp_multihop, password, timer_keepalive, timer_holdtime, min_neighbor_holdtime, update_source, soft_reconfiguration_inbound, send_community,inbound_route_map, outbound_route_map, next_hop_self. And also supports for removing BGP neighbor configuration. Any configuration within this scope, user only needs to update files in host_vars. For any other configuration out of this scope, it requires the ios_subplay playbook modification meet to the demands.  

#### How to use:
The only user input required will be to update the dictionary in host_vars to reflect what you want to configure on the devices. 
Provide inputs in the files under host_vars. Update the values as instructed below. 

Then run the playbook task_01_main.yml. If you are running the playbook via the command line on ansible box, please use: ansible-playbook -i inv.yml task_01_main.yml.

#### Input file format

    devicetype: ios
    neighbor: 7.7.7.7
    remote_as: 2
    description: bgp  test
    ebgp_multihop: 100
    password: password
    timer_keepalive: 300
    timer_holdtime: 360 # Hold time should be greater than the keepalive time
    min_neighbor_holdtime: 360
    update_source: lo0
    soft_reconfiguration_inbound: true
    send_community: true
    inbound_route_map: routemapin
    outbound_route_map: routemapout
    next_hop_self: false
    action: add



    ---
    # IOS
    # Add/remove new BGP neighbor to existing BGP process
    # action: add or remove
    # Mandatory Arg: (devicetype, neighbor, remote_as, action)
    # Optional Arg: (description, ebgp_multihop, password, timer_keepalive, timer_holdtime, min_neighbor_holdtime, update_source, soft_reconfiguration_inbound, send_community, inbound_route_map, outbound_route_map, next_hop_self)

    ## Arguments option ##
    #devicetype: 'ios' or 'nxos'
    #neighbor: [BGP neighbor IP address, eg. 7.7.7.7]
    #remote_as: [Remote AS of the BGP neighbor to configure. The range is from 1 to 4294967295, eg. 2]
    #description: [Neighbor specific description, eg. bgp test]
    #ebgp_multihop: [Specifies the maximum hop count for EBGP neighbors not on directly connected networks. The range is from 1 to 255, eg. 100]
    #password: [Password to authenticate the BGP peer connection. eg. password]
    #timer_keepalive: [Keepalive time. The range is from 0 to 65535. eg. 300]
    #timer_holdtime: [Holdtime. Hold time should be greater than the keepalive time. The range is from 0 to 65535. eg. 360]
    #min_neighbor_holdtime: [The minimum acceptable holdtime. Must be less than or equal to the holdtime. The range is from 0 to 65535. eg. 360]
    #update_source: [Source of the routing updates. eg. lo0]
    #soft_reconfiguration_inbound: 'true' or 'false' or 'nil'
    #send_community:  'true' or 'false' or 'nil'
    #inbound_route_map: [Route map name for incoming routes. eg. routemapin]
    #outbound_route_map: [Route map name for outgoing routes. eg. routemapout]
    #next_hop_self: 'true' or 'false' or 'nil'
    #action: 'add' or 'remove'



    ## eg. for adding BGP neighbor to existing BGP process ##
        ---

        bgp_Neighbor_commands:

          bgp_neighbor_1:
            devicetype: ios
            neighbor: 7.7.7.7
            remote_as: 2
            description: bgp  test
            ebgp_multihop: 100
            password: password
            timer_keepalive: 300
            timer_holdtime: 360 
            min_neighbor_holdtime: 360
            update_source: lo0
            soft_reconfiguration_inbound: true
            send_community: true
            inbound_route_map: routemapin
            outbound_route_map: routemapout
            next_hop_self: false
            action: add

          bgp_neighbor_2:
            devicetype: ios
            neighbor: 8.8.8.8
            remote_as: 3
            description: 
            ebgp_multihop: 
            password: 
            timer_keepalive: 
            timer_holdtime: 
            min_neighbor_holdtime: 
            update_source: 
            soft_reconfiguration_inbound: 
            send_community:
            inbound_route_map: 
            outbound_route_map: 
            next_hop_self: 
            action: add



    ## eg. for removing BGP neighbor from existing BGP process ##
        ---

        bgp_Neighbor_commands:

          bgp_neighbor_1:
            devicetype: ios
            neighbor: 7.7.7.7
            remote_as: 2
            description: bgp  test
            ebgp_multihop: 100
            password: password
            timer_keepalive: 300
            timer_holdtime: 360 
            min_neighbor_holdtime: 360
            update_source: lo0
            soft_reconfiguration_inbound: true
            send_community:
            inbound_route_map: routemapin
            outbound_route_map: routemapout
            next_hop_self: false
            action: remove

          bgp_neighbor_2:
            devicetype: ios
            neighbor: 8.8.8.8
            remote_as: 3
            description: 
            ebgp_multihop: 
            password: 
            timer_keepalive: 
            timer_holdtime: 
            min_neighbor_holdtime: 
            update_source: 
            soft_reconfiguration_inbound: 
            send_community:
            inbound_route_map: 
            outbound_route_map: 
            next_hop_self: 
            action: remove


### Return values
On completion, the playbook will output reports in the artefacts directory detailing the pre and post BGP configuration for each device that it executed for.
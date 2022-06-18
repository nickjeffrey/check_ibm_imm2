# check_ibm_imm2
nagios check for IBM / Lenovo Integrated Management Module 2 (IMM2)

# Requirements
perl, snmp

# Setup
You will need to enable SNMPv1 on the Integrated Management Module on the IBM/Lenovo server.
To enable SNMP from the web GUI:  IMM Management, Network, SNMP, Enable SNMPv1, community name, Apply
To enable SNMP from the CLI:      snmp -a on -c1 public -c1i1 0.0.0.0 -l "Datacenter Rack 123" -cn helpdesk@example.com

You will need to add a section similar to the following to the commands.cfg file on the nagios server.  
```
# 'check_ibm_imm2' command definition
   define command{
   command_name    check_ibm_imm2
   command_line    $USER1$/check_ibm_imm2 -H $HOSTADDRESS$ -c $ARG1$ 
   }
```

 You will need to add a section similar to the following to the services.cfg file on the nagios server.  
```
# Check IBM IMM2
# Requires SNMP enabled on IMM2
# syntax is check_ibm_imm2_snmp!optional_snmp_community
define service {
        use                             generic-service
        hostgroup_name                  all_imm
        service_description             IBM IMM2
        check_command                   check_ibm_imm2!optional_snmp_community
        }
```

 # Output
 You will see output similar to the following:
 ```
 IBM IMM2 OK - System_Health:Normal  Ambient_Temperature:19.0C  Power_Status:Normal  RAM:512GB  CPU_speed:2600Mhz  CPU_sockets:2  CPU_cores:12  CPU_threads:24   Model:8737-15X  Serial:21ARXXX UUID:7096C445CC4B11E3A7AB0090FA6AXXX  Description:IBM Flex System x240 
 ```
 

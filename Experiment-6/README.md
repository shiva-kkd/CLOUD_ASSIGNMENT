# Experiment 6: Simulate a Cloud Scenario Using CloudSim and Run a Scheduling Algorithm Not Present in CloudSim

## Aim
To simulate a cloud scenario using CloudSim and run a scheduling algorithm that is not present in CloudSim.

## Prerequisites
- Java JDK installed
- Eclipse IDE
- CloudSim installable files (downloaded and unzipped)

## Procedure

### Step 1: Download CloudSim
Download the CloudSim installable files from https://code.google.com/p/cloudsim/downloads/list and unzip them.

### Step 2: Open Eclipse
Launch the Eclipse IDE.

### Step 3: Create a new Java project
Go to **File** > **New** > **Java Project**.

### Step 4: Import CloudSim
Import the unpacked CloudSim project into the new Java project.

### Step 5: Initialize the CloudSim library
```java
CloudSim.init(num_user, calendar, trace_flag);
```

### Step 6: Create the data center
Data centers are the resource providers in CloudSim. Creating one needs a `DatacenterCharacteristics` object, which stores the architecture, OS, list of machines, allocation policy (time-shared or space-shared), time zone and price.

```java
Datacenter datacenter0 = new Datacenter(name, characteristics,
        new VmAllocationPolicySimple(hostList), storageList, 0);
```

### Step 7: Create the broker
```java
DatacenterBroker broker = createBroker();
```

### Step 8: Create the virtual machine
The constructor takes the VM ID, the owner's user ID, MIPS, number of PEs (CPUs), RAM, bandwidth, storage size, the VMM, and the cloudlet scheduler policy.

```java
Vm vm = new Vm(vmid, brokerId, mips, pesNumber, ram, bw, size, vmm,
        new CloudletSchedulerTimeShared());
```

### Step 9: Submit the VM list to the broker
```java
broker.submitVmList(vmlist);
```

### Step 10: Create the cloudlet
Specify the cloudlet's length, file size, output size and utilization models.

```java
Cloudlet cloudlet = new Cloudlet(id, length, pesNumber, fileSize,
        outputSize, utilizationModel, utilizationModel, utilizationModel);
```

### Step 11: Submit the cloudlet list to the broker
```java
broker.submitCloudletList(cloudletList);
```

### Step 12: Start the simulation
```java
CloudSim.startSimulation();
```

## Output (Sample from the existing example)

```
Starting CloudSimExample1...
Initialising...
Starting CloudSim version 3.0
Datacenter_0 is starting...
Broker is starting...
Entities started.
0.0: Broker: Cloud Resource List received with 1 resource(s)
0.0: Broker: Trying to Create VM #0 in Datacenter_0
0.1: Broker: VM #0 has been created in Datacenter #2, Host #0
0.1: Broker: Sending cloudlet 0 to VM #0
400.1: Broker: Cloudlet 0 received
400.1: Broker: All Cloudlets executed. Finishing...
400.1: Broker: Destroying VM #0
Broker is shutting down...
Simulation: No more future events
CloudInformationService: Notify all CloudSim entities for shutting down.
Datacenter_0 is shutting down...
Broker is shutting down...
Simulation completed.

========== OUTPUT ==========
Cloudlet ID    STATUS     Data center ID    VM ID    Time    Start Time    Finish Time
     0         SUCCESS         2             0       400        0.1          400.1
```

## Result
A cloud scenario was successfully simulated using CloudSim, and the cloudlet was executed successfully on the virtual machine.
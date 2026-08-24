##Virtual Machines
- VM Sizing:
 - B burstable
 - D general
 - E memory
 - F compute
 - M large memory
 - L storage
 - N GPU
  
 Standard_D2s_v5 = (D)General purpose + 2 vCPUs + (s)premium disk + (v5)hardware generation
  
  - VMSS - Virtual Machine Scale Sets - groups of identical, load-balanced VMs. Can automatically scale out or in based on demand of schedules.
  - VM Availability Sets - improve your resiliency inside a region. Reduce the chance that all VMs are affects by maintenance or failure. Availability Sets don't add cost. Instead you pay for the VMs.

- Azure Container Instances are a platform as a service (PaaS) offering. You upload your containers and the service runs them for you.
- Azure Container Apps remove the container management overheaed (PaaS) and also include built-in load balancing and scaling.
- Azure Kubernetes Service (AKS) is a container orchestration service that manages the lifecycle of containers. Where you're deploying a large number of containers (a fleet) AKS can make fleet management simpler and more efficient.
  
- Azure Functions - no need to keep resources running in order for your app to function. An event wakes the function. Functions are commonly used when you need to perform work in response to an event (REST request). Functions scale automatically. Can be stateless (default) or stateful (Durable Functions).
  
- Azure AI services provides prebuilt capabilities for common AI scenarios.
- Agentic AI patterns - combine an AI model with instructions, context, and tool use to complete multistep goals.
- Azure Machine Learning - when you need to build, train, and manage custom machine learning models.
- IoT and Edge services
  - Azure IoT Hub enables secure, bi-directional communication between cloud services and IoT devices.
  - Azure IoT Central provides simplified software as a service (SaaS) IoT platforms for solution builders.
  - Azure IoT Edge extends cloud capabilities to edge devices so some workloads can run closer to where the data is stored.
  

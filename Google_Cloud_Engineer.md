ASSOCIATE CLOUD ENGINEER CERTIFICATION STUDY MATERIAL

BEFORE CLOUD
1. Ahead of time planning
2. Peak cloud provisioning - Buy infrastructure everytime prior to peak load usage
3. . High cost of procurement

AFTER CLOUD
1. Renting resources when needed and releasing back when not in use
2. Personally, no need to maitain the physical data center

REGIONS AND ZONES
1. Farther the region higher the latency (Slowness)
2. If data center crashes -> Low availability
3. . We can have the sample application hosted on multiple regions to avoid downtime
4. Regions - Specific geographic location to host the resources
5. Advantages of Regions
	- High availability
	- Low latency
	- Global footprint (Serve customers residing on different side of the globe)
	- Adhrerence to Govt regulations (Data stored only in the specific region)
6. Within region if high availability is requires then Zones can be added
7. Each Region -> 3 or more Zones -> One or more discrete clusters (physical infra within a data center)
8. Zones in a region are connected to low latency links (If application is on Z1. and DB is Z2. still low latency can be achieved)
----------------------------------------------------------------------------------------------------------------------------

GCE (GOOGLE COMPUTE ENGINE)
1. To deploy applications on the cloud -> rent virtual servers (VM) on GCP -> GCE 
2. To provision and manage VMs
3. Load balancing and auto scaling
4. Horizontal scaling refers to adding additional nodes 
   *Vertical scaling describes adding more power to your current machines
5. Attach storage & network storage
6. Manage NW connectivity and configuration to VM instances
7. Create a VM
	- Name
	- Labels
	- Region, Zone
	- Machine Configuration (General Purpose, Compute Optimized, Memory Optimized)
	- Operating System
	- Firewall Configuration
8. Machine family
	- General Purpose (E2, N2, N2D, N1)
		- Best price-performance ratio
		- Web + Backend apps, Small - Medium DBs, Dev environments
		
	- Memory Optimized (M2, M1)
		- Ultra high memory workloads
		- Large in-memory databases and in-memory analytics

	- Compute Optimized (C2)
		- Compute intensive workloads
		- Gaming applications
9. Commands to run on the VM
	-- 
	sudo su
	apt update 
	apt install apache2
	ls /var/www/html
	echo "Hello World!"
	echo "Hello World!" > /var/www/html/indexhtml
	echo $(hostname)
	echo $(hostname -i)
	echo "Hello World from $(hostname)"
	echo "Hello World from $(hostname) $(hostname -i)"
	echo "Hello world from $(hostname) $(hostname -i)" > /var/www/html/indexhtml
	sudo service apache2. start 
	--
10. IP address 
 - VPC Network -> External IP addresses -> Reserve static address
 - VM is created in a specific zone (Regional IP to be set)
 - Static
	- Remains same even if VM is restarted
	- It remains attached even if VM is stopped
	- Manual deletion is necessary if not used
	- Incur costs even when not used, explicit release is needed
	- It can be switched to another VM instance in the same project 	
 - Ephemeral
	- Changes everytime VM is restarted
11. Instance template
	- Automate VM creation
	- Select machine type, image, labels, startup script
	- Once created it cannot be modified, but it can be cloned to modify
	- No cost in creating an instance template but incur costs when an instance is created
 - Reducing launch time with custom image
	- Installing OS patches and software at launch of VM instances increases boot up time
	- Create custom image with preinstalled OS patches and software
	- Custom can be created from an instance, peristent disk, snapshot, another image or file storage
	- Can be shared across projects
	- Corporate security standards can be added (Hardening an image)
	- The disk attached to a running instance is not recommended to create an image as filesystem integrity can't be guaranteed
 - Reducing Costs
	- Sustained use discounts (SUD): Automatic discounts applied for using resources for a longer period of time (20-50%)
	- Committed use discounts (CUD): Reserve ahead of time (1. or 3.  years)(70% based on machine type and GPUs)
	- Preemptible VMs - short duration execution (24hrs), automatically reclaimed by GCP due to system demands
 - Live Migration & Availability Policy
	- Running instance is migrated to another host in the same zone
	- Doesn't change any attributes or properties of the VM
	- Supported for instance with local SSDs
	- Not supported for GPUs and preemptible instances
	- Availability Policy: 
		- On host maintenance option is either to (default) migrate to another hardware or shutdown the instance
		- Automatic restart in case of non-user interruption
12. Pre-requisites to create any GCP resources
	 - Project
	 - Associated billing account
	 - Supported APIs enabled 
13.  By default all resources are shared among the customers of Google If a dedicated resource is required then a sole-tenant node is to 	 be created	
14. How to manage OS patch management across VMs - VM Manager -> OS Patch Management
15. How to login to VM instance to install a software -> SSH
16. Do not expose VM to the internet -> Do not assign external IP address
----------------------------------------------------------------------------------------------------------------------------

INSTANCE GROUPS AND CLOUD LOAD BALANCING
1. Group of VMs managed as a single entity
2. Two types of Instance Groups
	- Managed
		- Identical VMs created using a template
		- Auto scaling: Adds compute engine depending on the number of users (Load Balanced)
		- Auto healing: A health check; if an instance fails it will be auto replaced by a new one
		- Managed releases: Upgrade from one version to another without downtime
			- Rolling updates: Release new version step by step Upgrade only percentage of instances at a time
			- Canary deployment: Test new version with a group of instances before releasing it globally
	- Unmanaged
		- Different configurations for VMs in the same group
		- Does not offer auto scaling, healing & other services
3. Instance Groups can be zonal or regional
4. Updating the MIG
	- Rolling updates
		- When?
			- Proactive (Immediate)
			- Opportunisitc (When IG is resized)
		- How?
			- Max Surge: How many instances added at any point in time
			- Max Unavailable: How many instances can be offline during the update
	- Rolling restart/replace
		- No change in template but replace/restart the existing VMs
5. Cloud Load balancing
	- Distributes the user traffic across instances in single or multiple regions
	- Fully distributed software defined service
	- Health Check: Route to healthy instances
	- Auto scaling`
	- Global load balancing with single anycast IP
		- Supports internal load balancing
		- HTTP(S): Web Apps, Rest APIs
		- TCP 
		- UDP
	- SSL/TLS termination/offloading
		- Client to Load Balancer: HTTPS/TLS
		- Load Balancer to VMs: HTTP/TCP
	- LB Scenarios
		- Only healthy instances to receive the traffic: Health Check
		- High Availability: Multiple MIGs -> Multiple regions -> Load Balanced
		- Route requests to multiple microservices using same LB
			- Create individual MIGs and backend service for each microservice
			- Create host and path rules to redirect to specific microservice
			- Routing to a backend cloud storage is possible too
			- LB global HTTPs traffic across backend instances across multiple regions: External HTTPs LB
			- SSL termination for global non-HTTPs traffic with LB: SSL proxy LB
----------------------------------------------------------------------------------------------------------------------------

GOOGLE CLOUD SHELL
1. Backed by a VM instance, auto provisioned when launched.
2. 5GB free persistence storage (HOME dir).
3. Prepackaged with the latest version of Cloud SDK, Docker etc.
4. Files, config persists b/w sessions.
5. After 20 mins of inactivity changes made outside $HOME will be lost.
6. After 120 days on inactivity even $HOME dir is deleted.
7. SSH into VM using private IP.
8. core.project, compute.region, compute.zone.
----------------------------------------------------------------------------------------------------------------------------

MANAGED SERVICES IN GCP
1. IAAS (Infrastructure As A Service)
	- Use only infrastructure from cloud provider
	- Example: VMs to deploy the applications or DBs
	- We are responsible for
		- Application code and runtime
		- Load balancing
		- Auto scaling
		- OS upgrades and patches
		- Availability	
2. PAAS (Platform As A Service)
	- Platform provided by the cloud 
	- Cloud provider is responsible for
		- OS and patches
		- Application runtime
		- Auto scaling, Availability & Load Balancing
	- We are responsible for
		- Configuration of App & Services
		- Application code 
	- Example: Google App Engine
	- Varieties
		- CAAS (Container As A Service): Containers instead of Apps
		- FAAS (Function As A Service): Functions instead of Apps
		- DATABASES : CloudSQL, BigQuery, AI, ML etc 
	- Containers and Orchestration
		 - Supports usage of multiple technologies in a microservices model
		 - Docker Image: App code and dependencies, App runtime (JDK, NodeJS)
		 - Runs the same way on any infrastructure (Local, Data Center, Cloud)
		 - Docker images are lightweight compared to VMs as they don't need the guest OS
		 - Containers are isolated hence not dependent on each other
		 - Cloud neutral
		 - Features of Orchestration
			- Auto scaling of containers based on demand
			- Service discovery, finding one another (No need to manually harcode URLs in the app code)
			- LB
			- Self healing
			- Zero downtime deployments
	- GCE (IAAS): High performance and general purpose VMs that scale globally.
	- GKE (CAAS): Orchestrate containerized microservices Needs advanced cluster config and monitoring.
	- GAE (PAAS, CAAS, Serverless): Build higly scalable applications on a fully managed platform using open source and familiar languages	and tools.
	- CFs (FAAS): Build event driven applications using simple single purpose functions.
	- Cloud Run (CAAS Serverless): Develop and deploy highly scalable containerized apps. Cluster not needed.
----------------------------------------------------------------------------------------------------------------------------

GOOGLE APP ENGINE
1. Simplest way to deploy and scale applications in GCP.
2. Provides end-end app management.
3. Supports
	- Go, Java, NodeJs etc using pre-configured runtimes.
	- Use custom runtime - write in any language (Containers).
	- Connect to varitey of Google Cloud storage products.
4. No usage charges - Applicable only for resources provisioned.
5. Auto LB and scaling, platform updates, health monitoring.
6. Application versioning.
7. Traffic splitting.
8. Environments
	- STANDARD
		- Applications run in lang specific sandboxes.
		- Complete isolation from OS/Disk etc.
		- V1 (OLD VERSIONS): Java, Python, Go, PHP.
		- Only Python & PHP 
			- Restricted nw access.
			- Only whitelisted libs and extensions are allowed.
		- V2 (NEWER VERSIONS): Java, Python, NodeJS, Rub, Go.
		- Full nw access and no restrictions on libs/extns.
		- Pricing based on INSTANCE HOURS.
		- Scaling: Manual, Automatic, Basic (Adhoc load).
		- Scaling to Zero: Possible.
		- Instance startup time: Seconds.
		- Rapid Scaling: Yes.
		- Max timeout: 1-10 mins.
		- Local disk: Can write to /tmp except for Python/PHP.
		- SSH for debugging: No.		
	- FLEXIBLE
		- Makes use of GCE VMs.
		- Application instances run within docker containers.
		- Support any runtime.
		- Provides access to background processes and local disks.
		- Pricing based CPU, MEMORY AND PERISTENT DISKS.
		- Scaling: Manual, Automatic.
		- Scaling to Zero: Min 1 instance required. 
		- Instance startup time: Minutes.
		- Rapid Scaling: No.
		- Max timeout: 60 mins.
		- Local disk: New disk on every startup (Ephemeral).
		- SSH for debugging: Yes.
9. Application Component Hierarchy
	- Only one application per project.
	- Application can have multiple microservices or app components.
	- Each service can have a different versions & different settings.
	- Each version is associated with code and configuration.
	- Multiple versions can co-exist.
	- Option to rollback and split traffic.
10. Scaling instances
	- AUTOMATIC
		- Recommended for continuously running workloads.
		- Based on
			- CPU utilization threshold.
			- Throughput threshold.
			- Max concurrent requests.
		- Min and max instances can be configured.
	- BASIC
		- Instances are created as and when requests are received.
		- Instances are shutdown if zero requests, hence low usage costs.
		- Recommended for adhoc workloads.
		- High latency is possible.
		- Available config max instances and idle timeout.
	- MANUAL
		- Cofigure specific amount of instances to run.
11. 
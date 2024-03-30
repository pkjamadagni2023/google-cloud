ASSOCIATE CLOUD ENGINEER CERTIFICATION

REFERENCES
	https://github.com/in28minutes/course-material/blob/main/14-google-certified-professional-cloud-developer/downloads.md
	https://www.geeksforgeeks.org/difference-between-iaas-paas-and-saas/

BEFORE CLOUD
1. Ahead of time planning

2. Peak cloud provisioning - Buy infrastructure everytime prior to peak load usage.

3. High cost of procurement.

AFTER CLOUD
1. Renting resources when needed and releasing back when not in use.

2. Personally, no need to maitain the physical data center.

REGIONS AND ZONES
1. Farther the region higher the latency (Slowness)

2. If data center crashes -> Low availability.

3. We can have the sample application hosted on multiple regions to avoid downtime.

4. Regions - Specific geographic location to host the resources.

5. Advantages of Regions
	- High availability
	- Low latency
	- Global footprint (Serve customers residing on different side of the globe)
	- Adhrerence to Govt regulations (Data stored only in the specific region)

6. Within region if high availability is requires then Zones can be added

7. Each Region -> 3 or more Zones -> One or more discrete clusters (physical infra within a data center).

8. Zones in a region are connected to low latency links (If application is on Z1 and DB is Z2 still low latency can be achieved).

GCE (GOOGLE COMPUTE ENGINE)
1. To deploy applications on the cloud -> rent virtual servers (VM) on GCP -> GCE 

2. To provision and manage VMs.

3. Load balancing and auto scaling.

4. Horizontal scaling refers to adding additional nodes. 
   *Vertical scaling describes adding more power to your current machines.

5. Attach storage & network storage.

6. Manage NW connectivity and configuration to VM instances.

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
		- Web + Backend apps, Small - Medium DBs, Dev environments.
		
	- Memory Optimized (M2, M1)
		- Ultra high memory workloads.
		- Large in-memory databases and in-memory analytics

	- Compute Optimized (C2)
		- Compute intensive workloads.
		- Gaming applications.

9. 	Commands to run on the VM
	sudo su
	apt update 
	apt install apache2
	ls /var/www/html
	echo "Hello World!"
	echo "Hello World!" > /var/www/html/index.html
	echo $(hostname)
	echo $(hostname -i)
	echo "Hello World from $(hostname)"
	echo "Hello World from $(hostname) $(hostname -i)"
	echo "Hello world from $(hostname) $(hostname -i)" > /var/www/html/index.html
	sudo service apache2 start

10. IP address 
 - VPC Network -> External IP addresses -> Reserve static address
 - VM is created in a specific zone (Regional IP to be set)
 - Static
	- Remains same even if VM is restarted.
	- Manual deletion is necessary if not used.
	- Incur costs
 - Ephemeral
	- Changes everytime VM is restarted.

GOOGLE CLOUD SHELL
	- Backed by a VM instance, auto provisioned when launched.
	- 5 GB of free persistence storage (HOME dir)
	- Prepackaged with the latest version of Cloud SDK, Docker etc.
	- Files, config persists b/w sessions.
	- After 20 mins of inactivity changes made outside HOME will be lost.
	- After 120 days on inactivity even $HOME dir is deleted.
	- SSH into VM using private IP.
	- core.project, compute.region, compute.zone

MANAGED SERVICES IN GCP
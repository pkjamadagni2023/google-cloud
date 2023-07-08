                GOOGLE CLOUD PROFESSIONAL ARCHITECT CERTIFICATION
DAY 1
1. Peak load provisioning
	- Buy infra during peak load
	- Remains idle during low load and wasted
	- High cost
    - Ahead of time planning
	- Dedicated team to maintain

2. Cloud is an alternative which provides on demand provisioning or elasticity 
   that helps in variable expense

3. Go global in minutes, no need to spend money on maintaing the data centers

4. Services that use GCP - Gmail, Youtube 1 Billion users

5. It provides multiple services based on the requriement

6. Region and Zones
 - If data center is situated in a far region then we face high latency (slow 
   access) and low availability in case it crashes
 - Setting up data centers in multiple regions is not easy
 - Google provides 20+ regions expanding every year
 - High availability, low latency, global footprint, adhere to govt regulations  
   (data security)
 - To achieve high availability within the same region, zones will come to the rescue
 - Each region will have atleast 3 or more zones for high availability and fault tolerance
 - Each zone will have atleast one or more clusters (data centers)
 - The services can be split across zones and still get good latency

DAY 2
1. Google Compute Engine (GCE)
 - Deploy applications on premise requires virtual machine
 - Helps in creating and managing VMs
 - Load balancing and auto scaling multiple VMs
 - Attach storage
 - Manage network connectivity and config for the VMs

2. Compute Enginer Family
 - Choose hardware by machine type and choose software by image
 - Hardware
	- General purpose
		- Best price-performance ratio 
		- Web and App servers, small-medium DBs, Dev Servers
	- Memory optimize
		- Ultra high memory workloads
		- Large in-memory DBs and in-memory analytics
	- Compute Optimized
		- Compute intensive workloads
		- Gaming apps
 - OS
	- Image: Software on the VMs
		- Public image: Provided by google, open source or third party
 		- Custom image: Created by developer for the projects
		
3. External IP 
	- Internet accessible
	- It changes every time VMs are restarted. 
	- Prevents access to the VM
	- Quick way to assign static IP to have a constant IP
	- It is reserved and charged more even if VM is stopped
	- It should be released manually

4. Internal IP - Internal to GCP network

5. Simplify VM HTTP server setup
	- Startup script
		- Added as part of creating a VM step
		- Editable
	- Instance template
		- Previous approach is tedious in nature since every config is manually created
		- It cannot be updated once created
		- Clone existing template and create a new version
		- No costs in creating a template but would incur cost for creating a VM using it.
	- Custom image*
		- Installing OS updates and softwares during VM startup is time consuming
		- As a solution create a custom image with OS patches and softwares pre-installed
		- Can be created from an instance, persistent disk, snapshot, another image, file is cloud storage
		- Custom image can be shared across projects
		- Deprecate option available for obsolete images
		- Hardening an image: Customize to meet the corporate security standards
		- Compute Enginer -> Storage -> Disks -> Select VM and create an
		- Pre-requisite is to stop the VM before creating an image

6. A VM by default will share the hardware with other users as well. To have a dedicated hardware for an enterprise create a group in sole-tenant nodes and attach the affinity label while creating the VM.
---------------------------------------------------------------------------------
DAY 3
1. Instance Groups - Group of VMs managed as a single entity (same lifecycle)

2. Location of an instance group can be zonal or regional

3. Types of IGs
	- Managed
		- Identical VMs created using a template
		- Auto scaling: Increase/Decrease the instances based on the load
		- Auto healing: Constant helath check if one of the instances is down it will be auto replaced
		- Managed releases
		- Add load balancer to distribute the load
		- Create instance in multiple zones. 
		- Regional MIGs provides higher availability compared to Zonal
		- Rolling updates: Update only a percentage of instances at a time
		- Canary deployment: Test new version with a group of instances before releasing it for all
	- Un-Managed
		- VMs individually created with different config, hardware
		- No auto scaling, healing or other services

4. Create MIG
	- Instance template is mandatory
	- Auto Scaling
		- Min no. of instances
		- Max no. if instances
		- Metrics: CPU Utilization or Load Balancer Uitilization or other metric from Stack Driver
		- Cool-down period: How long to wait before checking the metrics again
		- Scale in Controls: Prevent suddent drop in no of VM instances (Either percentage or number)
	- Auto Healing
		- Health check
		- Initial delay to ensure check after the VM is up and running
---------------------------------------------------------------------------------
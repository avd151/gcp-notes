## Notes from questions

Q1. Every employee of your company has a Google account. Your operational team needs to manage a large number of instances on Compute Engine. Each member of this team needs only administrative access to the servers. Your security team wants to ensure that the deployment of credentials is operationally efficient and must be able to determine who accessed a given instance. What should you do?
- => Ask each member of the team to generate a new SSH key pair and to add the public key to their Google account. Grant the compute.osAdminLogin role to the Google group corresponding to this team.
- have users with the same responsibilities into groups and assigning IAM roles to the groups rather than individuals - manage groups via admin console
-  access can be given adding SSH public key to GCE -> mtadata => every instance will inherit the key
- use configuration mgmt tool to deploy google group to each instance => deploy private ssh keys => more efficient
- providing role to user/ groups => captured in audit logs => more secure

Q2. You need to create a custom VPC with a single subnet. The subnet's range must be as large as possible. Which range should you use? 
- => 10.0.0.0/8
- custom vpc subnet creation => min size = /8
- only the first 8 bits (out of 32 bits in an IPv4 address) are reserved for identifying the network part of the address => remaining 24 bits are available for host addresses within the network, which makes the subnet range large
- private network range defined by IETF-followed by all cloud providers => internal ip address ranges => 24 bit block = 10.0.0.0/8
- supported internal IP Address ranges are
1. 24-bit block 10.0.0.0/8 (16777216 IP Addresses) = 10.0.0.0 to 10.255.255.255
2. 20-bit block 172.16.0.0/12 (1048576 IP Addresses) = 172.16.0.0 to 172.31.255.255
3. 16-bit block 192.168.0.0/16 (65536 IP Addresses) = 192.168.0.0 to 192.168.255.255
- 0.0.0.0/0 = all possible IP addresses => invalid and not safe range for subnet - and is not private ip range

Q3. You want to select and configure a cost-effective solution for relational data on Google Cloud Platform. You are working with a small set of operational data in one geographic location. You need to support point-in-time recovery. What should you do?
- => Select Cloud SQL (MySQL). Verify that the enable binary logging option is selected. 
- binary logging option => point in time recovery (but reduces write performance) - restore your database to a specific point in time
- Cloud SQL = fully-managed relational database service - supports MySQL, PostgreSQL, and SQL Server - high availability, automatic backups, and point-in-time recovery - cost-effective solution for small sets of operational data in one geographic location
- cloud spanner - for large amount of data and multi region (global)

Q254. Security team member needs to see vulnerabilities, OS metadata for GCE instance having critical application 
- => steps = OS config agent installed on instance. member given roles/osconfig.vulnerabilityReportViewer - to view vulnerability data
- Ops agent = to collect system, application metrics, logs - monitor performance, health of applications, vm
- OS config agent = for OS configuration, inventory mgmt, vulnerability reporting - collect system level inventory info (packages installed), OS vulnerability
- osconfig.inventoryViewer role = access general OS metadata

Q255. To deploy new features to existing Cloud run service. Reduce no. of customers affected on outage with min cost. Manage revisions to existing service. 
- => steps = gradually roll out new revision. split customer traffic between revisions, in case of problem rollback changes
- deploy new features => split traffic
- can do above by - customers set exponential backoff at their end -> but adds cost for customer

Q256. external person need to access Linux GCE instance. he's connected via VPN connection to my network, but does not have google accnt.
- => steps = external person generate SSH key pair. public key(can be shared) from it added to instance. person access instance by ssh with private key(needs to be secure)
- IAP = identity aware proxy - helpful if application already uses external authentication system like google account

Q257. monitor unexpected firewall changes and gce instance creation in GCP 
- => steps = use cloud logging filters - create log based metrics for firewall, instance actions. monitor that metrics, set alerts
- bigquery log sink - used for routing large amt of logs at given place (store logs)

Q258. configuring service accounts for multiple projects. web-app project VMs need access to bigquery datasets in crm project.
- => give bigquery.dataViewer role to crm-databases, appropriate roles to web-app project. 
- dont give any service account project owner role directly  use principle of least privelege - separation of concerns between projects
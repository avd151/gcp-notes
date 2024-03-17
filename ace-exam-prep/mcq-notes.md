## Notes from questions

Q1. company - all employees have google account. manage any GCE instances. all ops team members need admin access to servers. efficient deployment of credentials + access + we keep record that who is given what access ?
- => each member of team generates new SSH key pair. add public key to their Google accnt. give compute.osAdminLogin role to ops team google group
- way 2 also works - generate new ssh key pair. give private key to member. configre public key at project level. allow project wide public ssh keys on each instance
- use configuration mgmt tool to deploy google group to each instance => deploy private ssh keys => more efficient
- providing role to user/ groups => captured in audit logs => more secure

Q2. custom vpc with 1 subnet. create largest subnet? 
- => 10.0.0.0/8
- custom vpc subnet creation => min size = /8
- private network range defined by IETF => internal ip address ranges => 24 bit block = 10.0.0.0/8

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
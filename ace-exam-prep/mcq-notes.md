## Notes from questions
Q. Security team member needs to see vulnerabilities, OS metadata for GCE instance having critical application 
- => steps = OS config agent installed on instance. member given roles/osconfig.vulnerabilityReportViewer - to view vulnerability data
- Ops agent = to collect system, application metrics, logs - monitor performance, health of applications, vm
- OS config agent = for OS configuration, inventory mgmt, vulnerability reporting - collect system level inventory info (packages installed), OS vulnerability
- osconfig.inventoryViewer role = access general OS metadata

Q. To deploy new features to existing Cloud run service. Reduce no. of customers affected on outage with min cost. Manage revisions to existing service. 
- => steps = gradually roll out new revision. split customer traffic between revisions, in case of problem rollback changes
- deploy new features => split traffic
- can do above by - customers set exponential backoff at their end -> but adds cost for customer

Q. external person need to access Linux GCE instance. he's connected via VPN connection to my network, but does not have google accnt.
- => steps = external person generate SSH key pair. public key(can be shared) from it added to instance. person access instance by ssh with private key(needs to be secure)
- IAP = identity aware proxy - helpful if application already uses external authentication system like google account

Q. monitor unexpected firewall changes and gce instance creation in GCP 
- => steps = use cloud logging filters - create log based metrics for firewall, instance actions. monitor that metrics, set alerts
- bigquery log sink - used for routing large amt of logs at given place (store logs)

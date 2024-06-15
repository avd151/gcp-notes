Q1.  You have a Dockerfile that you need to deploy on Kubernetes Engine. What should you do?
- => Use kubectl app deploy <dockerfilename>
- it packages application -> docker container image -> run container on k8s (GKE) cluster -> can deploy application as load balanced set of replicas that scale acc to users
- pricing calculator = find cost estimate of project - billing enabled on project level
- cloud shell activated => shell/ command prompt window enabled

Q2. You need to create a custom VPC with a single subnet. The subnet's range must be as large as possible. Which range should you use?
- => 10.0.0.0/8

Q3. You want to select and configure a cost-effective solution for relational data on Google Cloud Platform. You are working with a small set of operational data in one geographic location. You need to support point-in-time recovery. What should you do?
- =>  Select Cloud SQL (MySQL). Verify that the enable binary logging option is selected.
- used for restoring instance from backup/ PITR = point in time recovery - can do in Cloud SQL Enterprise edition and Cloud SQL Enterprise Plus edition
- instance restored => databases, users fro primary instance are restored to new instance - flags not restored => instance restarts after restoring
- flags previously set on the target instance are retained after the restore
- PITR - recover instance to specific point in time - always creates new instance - cannot perform on existing instance - for new instance to inherit source instance settings, the instance's state must be RUNNABLE - create Cloud SQL instance via GCP console => PITR enabled by default 
- PITR uses binary logging to archive logs

Q4. You want to configure autohealing for network load balancing for a group of Compute Engine instances that run in multiple zones, using the fewest possible steps. You need to configure re-creation of VMs if they are unresponsive after 3 attempts of 10 seconds each. What should you do? 
- => Create a managed instance group. Set the Autohealing health check to healthy (HTTP)
- health checks for autohealing and load balancing should be different
- Health checks for load balancing detect unresponsive instances and direct traffic away from them - Ensures that requests are sent only to instances that are up and running
- Health checks for autohealing (in MIG) detect and recreate failed instances - recreating VM instances when needed
- using same health check for services removes difference between unresponsive and failed instances => more latency, unavailability
- MIG = managed instance groups = group of homogeneous CE instances - managed as 1 entity - to distribute traffic, high availability - autohealing for n/w load balancing - health check will periodically probe the instances in the group to see if they are responding

Q5. You are using multiple configurations for gcloud. You want to review the configured Kubernetes Engine cluster of an inactive configuration using the fewest possible steps. What should you do?
- => Use kubectl config use-context and kubectl config view to review the output.

Q6. Your company uses Cloud Storage to store application backup files for disaster recovery purposes. You want to follow Google's recommended practices. Which storage option should you use?
- => Coldline Storage

Q7. Several employees at your company have been creating projects with Cloud Platform and paying for it with their personal credit cards, which the company reimburses. The company wants to centralize all these projects under a single, new billing account. What should you do?
- => In the Google Cloud Platform Console, create a new billing account and set up a payment method.
# Chef Server Platform Extension
This platform extension spins up a blank Chef server with Chef 12 installed making use of the AWS-type platform extension. 

The following additional Chef features are free for up to 25 nodes:

* High Availability. Ensure that your Chef service is uninterrupted within your data center or AWS region, even if a Chef server fails.
* Reporting. Capture and visualize what happens during the execution of chef-client runs across all of your Chef-managed infrastructure.
* Management Console. Use the web-based management console to manage RBAC, edit and delete nodes, and reset private keys. Keep up to date with what’s happening during chef client runs across an entire organization or on specific nodes.
* Analytics Platform. Get visibility into your Chef servers, verify compliance and keep up with changes, all with the Chef analytics platform.

Open source features beyond Chef server core include:

* Push Jobs. Execute commands across hundreds or even thousands of nodes in your Chef-managed infrastructure.

## Getting Started

Follow the platform extension loading instructions below:
```
services/<the hosting provider where you want the platform extension to be loaded>/README.md
```

Once the platform extensino has been loaded, the chef server will be proxied over port 443 from Nginx and is accessible over HTTPS. 

The default access credentials for the chef server web UI (once you have loaded the platform extension) are as follows:

 * username: admin
 * password: admin@1



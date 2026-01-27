1.Go to the below link and open the draw.io
https://aws.amazon.com/architecture/icons/

## Single Tier 


<img width="872" height="813" alt="image" src="https://github.com/user-attachments/assets/97a5b081-3402-485f-8976-29aa3e60dee6" />

https://app.diagrams.net/?splash=0&libs=aws4#LAWS.drawio#%7B%22pageId%22%3A%22AtUbVxGUSyG2jZwX1XyJ%22%7D


- When a user connects to an EC2 instance via a domain name (like www.example.com), they hit Route 53 first to perform a DNS lookup. 
- The Internet Gateway (IGW) is only involved after the user's computer has obtained the IP address and begins the actual data transfer (HTTP/SSH).

- Amazon Route 53 is a globally distributed service that operates above the level of a single VPC or Availability Zone (AZ). It is designed as a foundational, highly available, and resilient service that manages DNS for all of AWS, spanning multiple Regions

- An AWS Internet Gateway (IGW) sits at the VPC level, not at the Availability Zone (AZ) level. It is a highly available, horizontally scaled, and redundant VPC component that spans all Availability Zones within a region to allow communication between instances in public subnets and the internet. 



# Router 53 (R53)
If you are connecting via a Public IP address, Route 53 is not required.
The user's computer already has the "coordinates" (the IP) needed to find the AWS Internet Gateway, so it skips the DNS lookup phase entirely.
However, even if you can connect directly, an AWS expert would still use Route 53 for these specific professional use cases:
1. Management of Dynamic IPs
EC2 Public IPs can change if an instance is stopped and started. By using Route 53, you can map a friendly name (e.g., dev.example.com) to the IP. If the IP changes, you just update the DNS Record once, and users don't have to memorize a new string of numbers.

2. Private DNS (Internal Networking)
Inside a VPC, you might have microservices talking to each other. Instead of hardcoding
"10.0.0.5", you use a Route 53 Private Hosted Zone to create names like db.internal. This makes your infrastructure portable and easier to read.

3. Disaster Recovery & Health Checks
If you connect via IP and the instance crashes, the connection simply fails. If you use Route 53 with Health Checks, Route 53 can automatically "swing" that domain name to a backup instance's IP without the user ever knowing there was a failure.

4. Routing Policies
You can't do "logic" with a raw IP. Route 53 allows you to use Weighted Routing (sending 10% of traffic to a new test instance) or Latency Routing (sending users to the closest IP geographically).
The Expert Verdict:
Connecting by IP is fine for a quick test, but it is a "no-go" for production. It lacks the flexibility, failover capabilities, and human-readability that Route 53 provides.


# Internet Gateway

1. Internet Gateway (IGW): The packets reach the Internet Gateway attached to your VPC. This is the "front door" that allows external traffic to enter the private AWS network.

## Singel Tier HA


<img width="827" height="902" alt="image" src="https://github.com/user-attachments/assets/34a4aad4-3eaf-4724-99b7-032c4a1bcd31" />


https://app.diagrams.net/?splash=0&libs=aws4#LAWS.drawio#%7B%22pageId%22%3A%220I14I2eF0IdvqhJJ3Y2r%22%7D



## Auto Scaling


<img width="1320" height="744" alt="image" src="https://github.com/user-attachments/assets/7f514a47-7893-4727-94c6-c0350058e259" />


https://app.diagrams.net/?splash=0&libs=aws4







## ECR and ECS
<img width="1195" height="630" alt="image" src="https://github.com/user-attachments/assets/b10b53dd-2b29-47f3-b964-92f356e408a0" />








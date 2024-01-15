# Performance and Networking - EC2/Global Accelerator/ Cloud Front

# Step 1: Launching the EC2 instances

- Number of instances will be equal to three and search for the Wordpress image in the AMI search.

![Fig:1](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled.png)

Fig:1

- Select this image shown below:

![Fig:2](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%201.png)

Fig:2

- Select t2.micro
- Select “Proceed without a key pair”
- Edit the Network settings,  Select the default VPN  and select a Subnet (this is done to avoid the AZ variations)
- Make sure the Auto-assign IP is enabled
- In the Firewall (Security Groups) - Remove both the HTTPS and SSH rules.
- Create another Security group rule - Type shall be “All ICMP IPv4” and the source shall be “0.0.0.0/0”

![Fig:3](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%202.png)

Fig:3

- Rename the instances as shown below:

![Fig:4](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%203.png)

Fig:4

- Copy the public IP of any of the instances and add “http:// + IP address” this is to check if the instances is working.

# Step 2: Configuring Global Accelerator

- Give Accelerator a name.
- IP address shall be IPv4
- In the next step add the listeners:

![Fig:5](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%204.png)

Fig:5

- Next step is important where you select the region where the instances was created:

![Fig 6](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%205.png)

Fig 6

- In the next step select the EC2 instance which was named after Global Accelerator.

![Fig:7](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%206.png)

Fig:7

# Step 3: Setting up CloudFront

- Copy the “Public IPv4 DNS” name of the EC2 instances under the name of CloudFront and paste it in the orgin domain. Select the protocol as HTTP only.

![Fig:8](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%207.png)

Fig:8

- Under “**Default cache behavior”** change “Compress objects automatically” to No. Also select the settings shown below:

![Fig:9](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%208.png)

Fig:9

# Further Steps

- Copy the “Public IPv4 DNS” of the “Wordpress - Standard” instance and open in a new tab.
- Similarly, copy the DNS name of the Global Accelerator EC2 and open in a new tab. Copy the domain name of CloudFront and open it in a separate tab.
- Tracing the standard EC2

![Fig:10](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%209.png)

Fig:10

- Tracing the Global Accelerator EC2

![Fig:11](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%2010.png)

Fig:11

- Tracing the CloudFront EC2

![Fig:12](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%2011.png)

Fig:12

- For more detailed presentation, lets open an incognito window and and disable the cache:

![Fig:13](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%2012.png)

Fig:13

- Performance of standard EC2

![Fig:14](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%2013.png)

Fig:14

- Performance of Global Accelerator EC2

![Fig:15](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%2014.png)

Fig:15

- Performance of CloudFront

![Fig:16](Performance%20and%20Networking%20-%20EC2%20Global%20Accelerato%20c049cbf8b7e24aaa99c67221574847df/Untitled%2015.png)

Fig:16

- From the above comparison we can infer that:
    - Global accelerator and the CloudFront gives improved network performance.
    - They both use the edge locations (**A site that CloudFront uses to cache copies of your content for faster delivery to users at any location)**.
    - CloudFront uses the cache and for both HTTP and HTTPS traffic.
    - Global Accelerator is more of a general purpose tool. (Improved performance: **AWS
     Global Accelerator ingresses traffic from the edge location that is 
    closest to your end clients through anycast static IP addresses**.)
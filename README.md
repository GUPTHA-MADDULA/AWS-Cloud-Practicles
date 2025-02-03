<h1> AWS VPC Project with Public and Private Subnets </h1>

<h2> 📌 Overview </h2>
<p>
This project demonstrates how to set up an <strong>AWS Virtual Private Cloud (VPC)</strong> with both 
<strong>Public and Private Subnets</strong>. The architecture ensures a secure, scalable, and high-performing 
network environment for deploying cloud applications. 
</p>

<h2> 🔹 VPC Architecture </h2>

<h3> 1️⃣ Public Subnet </h3>
<ul>
    <li> Contains internet-facing resources like EC2 instances or Load Balancers. </li>
    <li> Connected to an <strong>Internet Gateway (IGW)</strong> for external access. </li>
</ul>

<h3> 2️⃣ Private Subnet </h3>
<ul>
    <li> Hosts internal resources such as databases and application servers. </li>
    <li> Not directly accessible from the internet. </li>
    <li> Uses a <strong>NAT Gateway</strong> for outbound traffic to the internet. </li>
</ul>

<h3> 3️⃣ Internet Gateway (IGW) </h3>
<ul>
    <li> Enables internet access for resources inside the <strong>public subnet</strong>. </li>
</ul>

<h3> 4️⃣ NAT Gateway </h3>
<ul>
    <li> Allows outbound internet access from the <strong>private subnet</strong> while keeping it secure. </li>
</ul>

<h3> 5️⃣ Route Tables </h3>
<ul>
    <li> Defines routing rules for subnets. </li>
    <li> The Public Subnet routes traffic to the <strong>Internet Gateway</strong>. </li>
    <li> The Private Subnet routes external traffic through the <strong>NAT Gateway</strong>. </li>
</ul>

<h3> 6️⃣ Security Groups & NACLs </h3>
<ul>
    <li> <strong>Security Groups (SGs):</strong> Control inbound and outbound traffic at the instance level. </li>
    <li> <strong>Network ACLs (NACLs):</strong> Provide subnet-level security with rule-based access control. </li>
</ul>

<h2> 🚀 Deployment Steps </h2>
<h3> 1️⃣ Create a VPC </h3>
<pre>
aws ec2 create-vpc --cidr-block 10.0.0.0/16
</pre>

<h3> 2️⃣ Create Public & Private Subnets </h3>
<pre>
aws ec2 create-subnet --vpc-id vpc-12345678 --cidr-block 10.0.1.0/24 --availability-zone us-east-1a
aws ec2 create-subnet --vpc-id vpc-12345678 --cidr-block 10.0.2.0/24 --availability-zone us-east-1b
</pre>

<h3> 3️⃣ Attach Internet Gateway & NAT Gateway </h3>
<pre>
aws ec2 create-internet-gateway
aws ec2 attach-internet-gateway --internet-gateway-id igw-12345678 --vpc-id vpc-12345678

aws ec2 allocate-address
aws ec2 create-nat-gateway --subnet-id subnet-12345678 --allocation-id eipalloc-12345678
</pre>

<h3> 4️⃣ Configure Route Tables </h3>
<pre>
aws ec2 create-route-table --vpc-id vpc-12345678
aws ec2 create-route --route-table-id rtb-12345678 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-12345678
</pre>

<h3> 5️⃣ Launch EC2 Instances </h3>
<pre>
aws ec2 run-instances --image-id ami-12345678 --count 1 --instance-type t2.micro --subnet-id subnet-12345678
</pre>

<h2> 🔒 Security Best Practices </h2>
<ul>
    <li> <strong>Restrict SSH Access:</strong> Allow SSH only from trusted IPs. </li>
    <li> <strong>Enable VPC Flow Logs:</strong> Monitor traffic for security analysis. </li>
    <li> <strong>Use IAM Roles:</strong> Grant least privilege access. </li>
</ul>

<h2> 🛠 Future Enhancements </h2>
<ul>
    <li> Deploy Auto Scaling for better resource management. </li>
    <li> Integrate a Load Balancer for traffic distribution. </li>
    <li> Implement Terraform for Infrastructure-as-Code (IaC). </li>
</ul>

<h2> 📌 Conclusion </h2>
<p>
This project provides a foundational understanding of AWS networking, 
helping to build a <strong>secure and scalable cloud infrastructure</strong>. 
Feel free to enhance and expand based on your use case!
</p>

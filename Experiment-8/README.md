# Experiment 8: Deploy Dynamic Web Application on EC2 Instance on AWS

## Aim
To deploy a dynamic web application on an EC2 instance on AWS.

## Prerequisites
- An active AWS account
- A web browser with internet access

## Procedure

### Part A: Launch the EC2 Instance

**Step 1: Launch an instance**
Type **EC2** in the AWS search box and click on it. When the EC2 page opens, click **Launch instance**.

**Step 2: Name and tags**
Under **Name and tags**, give any name, e.g., `web-server`.

**Step 3: Application and OS image**
Under **Application and OS Images**, select **Amazon Linux**.

**Step 4: Instance type**
Under **Instance type**, select `t3.micro`.

**Step 5: Key pair**
Click **Create new key pair**, give it a name (e.g., `kyp`) and click **Create key pair**. The key pair file (`kyp.pem`) is downloaded automatically.

**Step 6: Network settings**
- Make sure **Allow SSH traffic from** is enabled.
- Tick the checkbox **Allow HTTPS traffic from the internet**.
- Tick the checkbox **Allow HTTP traffic from the internet**.

**Step 7: Storage and advanced details**
Keep **Configure storage** and **Advanced details** as they are.

**Step 8: Launch**
Click **Launch instance**.

### Part B: Connect to the Instance

**Step 1:** After successful launch, click **Instances**.

**Step 2:** Select the checkbox of the newly created instance (`web-server`) and click **Connect**.

**Step 3:** Under **Connect**, select the **EC2 Instance Connect** method and click **Connect**.

### Part C: Install the Web Server and Deploy the Website

Type the following commands in the terminal that opens:

```bash
# Switch to root user
sudo su -

# Update the packages
yum update -y

# Install the httpd (Apache) web server
yum install -y httpd

# Create a temporary folder
mkdir temp
cd temp

# Download the website template files
wget https://templatemo.com/download/templatemo_596_electric_xtra
ls -lrt

# Unzip the template
mkdir templatemo_596_electric_xtra_unzipped
unzip templatemo_596_electric_xtra -d templatemo_596_electric_xtra_unzipped
cd templatemo_596_electric_xtra_unzipped
ls -lrt

cd templatemo_596_electric_xtra
ls -lrt

# Copy the extracted files to the web server's root directory
mv * /var/www/html/
cd /var/www/html/
ls -lrt

# Check the status of the httpd server
systemctl status httpd

# Enable the httpd server
systemctl enable httpd

# Start the httpd server
systemctl start httpd
```

### Part D: Access the Website

1. Go to **Instances** in the EC2 console.
2. Select your instance and copy its **Public IPv4 address**.
3. Open a new browser tab, paste the public IP address and press Enter.

```
http://<public-ipv4-address>
```

## Output
The web page (the downloaded template website) opens in the browser using the public IP of the EC2 instance.

## Result
A web application was successfully deployed on an AWS EC2 instance using the Apache (httpd) web server and accessed through the instance's public IP address.


<img width="1040" height="336" alt="Screenshot 2026-10-07 235255" src="https://github.com/user-attachments/assets/edcfd730-8c0e-41b0-8f30-108e52a27146" />

<img width="1045" height="455" alt="Screenshot 2026-10-07 235236" src="https://github.com/user-attachments/assets/49559352-91e2-4151-817c-2655205a3fd0" />


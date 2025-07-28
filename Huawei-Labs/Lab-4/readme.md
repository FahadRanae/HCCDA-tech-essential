# Lab 4
Huawei Deep seek installation 
🤖 Lab: Deploying and Running DeepSeek on Huawei Cloud

This lab demonstrates how to deploy and run the DeepSeek 1.5B model using Ollama on a Huawei Cloud ECS. The lab includes creating an ECS, installing Ollama, downloading the DeepSeek model, and starting inference.

🎯 Objectives

Create and access an ECS instance

Install and configure Ollama

Deploy DeepSeek-R1 1.5B model

Start the model server and interact with it

📌 Prerequisites

Lab exercise account credentials

Access to Lab Desktop from Huawei Cloud console

Internet connectivity

🖥️ 1. Preparing the Lab Environment

1.1 Creating an ECS

Log in to Huawei Cloud and search ECS in the Service List.

Click Buy ECS, then go to Custom Config.

Configure the following:

Billing Mode: Pay-per-use

Region: AP-Singapore

Architecture: x86

Flavor: c6.xlarge.2 (4 vCPUs, 8 GiB RAM)

Image: CentOS 8.2 64bit (40 GiB)

Network Settings:

VPC: Use default or create new

Security Group: Use default or create new

EIP: Auto assign, Dynamic BGP, Traffic billing, 100 Mbit/s bandwidth

Instance Management:

ECS Name: ecs-cent

Password: Huawei1234%

Click Submit, then Agree and Submit.

1.2 Logging in to ECS

Use CloudShell from Huawei Cloud Lab Desktop

Enter the password Huawei1234% and connect to the instance

📦 2. Installing Ollama

Ollama helps run and manage LLMs locally. Two installation methods are provided:

🔸 Solution 1: Install via GitHub

curl -fsSL https://ollama.com/install.sh | sh
ollama -v  # check installation

If download fails, retry or use Solution 2.

🔸 Solution 2: Install from OBS Backup

wget https://sandbox-experiment-files.obs.cn-north-4.myhuaweicloud.com/deepseek/ollama-linux-amd64.tgz
sudo tar -C /usr -xzf ollama-linux-amd64.tgz
sudo chmod +x /usr/bin/ollama

# Check or create ollama user
test $(id -u ollama) || sudo useradd -r -s /bin/false -m -d /usr/share/ollama ollama

# Create ollama service
cat << EOF | sudo tee /etc/systemd/system/ollama.service
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
ExecStart=/usr/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3

[Install]
WantedBy=default.target
EOF

# Start service
sudo systemctl daemon-reload
sudo systemctl enable ollama
sudo systemctl start ollama
ollama -v  # verify installation

🧠 3. Deploying DeepSeek-R1 1.5B Model

DeepSeek is a powerful LLM supported by Ollama. Two deployment methods are available:

🔹 Solution 1: Pull Model Using Ollama (Community Version)

ollama pull deepseek-r1:1.5b
ollama run deepseek-r1:1.5b

⚠️ May take longer. If interrupted, rerun as Ollama supports resumable download.

🔹 Solution 2: Download Model from OBS Backup (Recommended)

wget https://sandbox-experiment-files.obs.cn-north-4.myhuaweicloud.com/deepseek/ollama_deepseek_r1_1.5b.tar.gz
sudo tar -C /usr/share/ollama/.ollama/models -xzf ollama_deepseek_r1_1.5b.tar.gz

cd /usr/share/ollama/.ollama/models
mv ./deepseek/sha256* ./blobs
mkdir -p ./manifests/registry.ollama.ai/library/deepseek-r1
mv ./deepseek/1.5b ./manifests/registry.ollama.ai/library/deepseek-r1
rm -rf deepseek/

# View model list
ollama list

# Run model
ollama run deepseek-r1:1.5b

🧪 Final Testing

If the model starts successfully, you will be able to interact with DeepSeek directly from the terminal.

> Hello DeepSeek!
> /bye  # to stop the session

📝 Notes

Always verify model version and service status using ollama -v and systemctl status ollama

Ensure sufficient bandwidth (100 Mbps) for smooth downloads

Use Solution 2 for faster setup during labs

📁 Screenshots & Artifacts

<img width="975" height="419" alt="image" src="https://github.com/user-attachments/assets/a80111af-97a9-41d4-8b4b-3c092cbaf4c4" />
<img width="975" height="355" alt="image" src="https://github.com/user-attachments/assets/3cdf5e55-82c5-4641-afe6-8917d9391021" />
<img width="975" height="692" alt="image" src="https://github.com/user-attachments/assets/b3b78466-5c7c-49e9-969c-3ca7136b41bb" />
<img width="975" height="252" alt="image" src="https://github.com/user-attachments/assets/0435278d-a91c-4ef8-afc9-25751c2c6997" />



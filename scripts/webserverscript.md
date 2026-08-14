# Deploying the Frontend Application

# Installing Unzip

echo "Installing unzip"

sudo apt update -y
sudo apt install unzip -y

echo "Download Fronted Template"
cd webserver

wget https://templatemo.com/tm-zip-files-2020/templatemo_520_highway.zip 

unzip templatemo_520_highway.zip

sudo cp -r templatemo_520_highway/* /home/ubuntu/webserver

Readme for Todo App 📝
Installation 🚀
Install Node.js and NPM on Ubuntu:
Make sure you have Node.js 16.x and NPM installed on your machine. If not, you can install them using the following commands:
curl -s https://deb.nodesource.com/setup_16.x | sudo bash
sudo apt install nodejs -y
Configuration ⚙️
Update Backend URL:
Open the src/TodoApp.js file.
Locate the variable storing the backend URL and update it with the appropriate value. (* See Below for PrivateIp Configuration)
Building and Running 🏗️
Install Dependencies:

Run the following command to install project dependencies:
npm install
Build the Project:

Execute the following command to build the project:
npm run build
Deployment 🚀
Deploy to Nginx Server:
Copy the generated artifacts from the build process.
Deploy the artifacts to your Nginx server. Ensure that the server is properly configured to serve the application.
* Using Private IP on the Backend VM 🌐
To use a Private IP on the Backend VM, follow the steps below:

1. Configure NGINX on the Backend VM ⚙️
Open the NGINX configuration file:

sudo nano /etc/nginx/sites-available/default
2. Insert Proxy Configuration 🔄
Copy and paste the following code just above the root /var/www/html line:

location /api {
   proxy_pass http://<PrivateIP of BackendVM>:8000;
   proxy_set_header Host $host;
   proxy_set_header X-Real-IP $remote_addr;
   proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
   proxy_set_header X-Forwarded-Proto $scheme;
}
Replace <PrivateIP of BackendVM> with the actual Private IP address of your Backend VM.

3. Update Frontend Configuration ⚙️
Open the src/TodoApp.js file in your frontend project.

Update the Backend URL by replacing the existing line with the following:

const API_BASE_URL = 'http://<FrontendVM Public IP>:80/api';
Replace <FrontendVM Public IP> with the actual Public IP address of your Frontend VM.

Important Note 📌
Make sure to restart NGINX on the VM after making the changes:

sudo service nginx restart
These configurations enable communication between the Frontend and Backend using Private IP on the Backend VM. Ensure that the IPs and ports are correctly set to match your environment.

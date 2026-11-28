Git Commands:
============
git init
git add .
git branch
git branch -M main # If branch name in local is master and in remote main 
git remote add origin https://github.com/ashok-khatua56/devops.git
git remote set-url origin https://github.com/ashok-khatua56/devops.git
git push -u origin main # For the first time.
git add . # for new file or midification of existing file
git commit -m "Your message"
git push origin main
git status
git restore
git revert
git reset
git clone
git branch 
git branch checkout
git branch -b
git switch -c
git branch D
git fetch origin
git merge origin/main safe for developer to use to avoid conflict
git pull origin main #combination of fetch and merge 
git diff
git diff commitHash1 commitHash2
git diff origin/main
git commit -a -m "commit message"
git stash
git stash list
git stash apply
git stash apply stash@{0}
git stash pop # Permanent restore
git stash clear
git config --global --unset user.name
git config --global --unset user.email

AWS Commands:
============
ssh -i "Path of the .pem file" username@ipAdress 
If permission denied in windows system then
icacls "Your .pem file name"
icacls 	"Your .pem file name" /inheritance:r
icacls "Your .pem file name" /remove:g "Administrators" "SYSTEMS", "USER"
icacls "Your .pem file name" /grant:r "$($env:Username):R"

Apache Web Server:
=================
sudo yum install httpd
sudo systemctl start httpd
sudo systemctl enable httpd
Add your project inside /var/www/html/
sudo systemctl stop httpd
sudo systemctl disable httpd

NGINX Web Server:
================
sudo yum update -y
sudo dnf install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
sudo systemctl stop nginx
sudo systemctl restart nginx

Node Set up:
===========
curl -fsSl https://rpm.nodesource.com/setup_20.x | sudo bash -
sudo dnf install nodejs -y
scp -i "path of your .pem file" -r "path of your nodejs project files" ec2-user@ipAddress:/home/ec2-user
cd "To your project path"
npm i
sudo npm install -g pm2
pm2 start index.js
pm2 startup
pm2 save
pm2 status

Configure nginx:
sudo nano /etc/nginx/nginx.conf
	location / {
        proxy_pass http://localhost:5000; #Your node server port
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
Add these lines of code after /etc/nginx/default.d/*.conf;

Ansible:=>
=======
sudo apt install ansible -y
ansible --version
1.Create Inventory File-
touch hosts
	[local]
	localhosts ansible_connection=local
ansible all -i hosts -m ping
2.Create Playbook file
touch create_file.yml
	---
	- name:Create a file using environment path
	  hosts: local
	  task: 
	    - name: Create ansible_file.txt
	      file:
		path: "{{ansible_env.HOME }}/ansible_file.txt"	
		state: touch
		mode: '0644'
ansible-playbook -i hosts create_file.yml

Roles:
=====
ansible-galaxy init nginx-role


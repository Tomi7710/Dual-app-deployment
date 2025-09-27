## Dual Application Deployment

This project showcases the deployment of a Flask app and a Node.js app using a shared PostgreSQL database.

### Workflow

Ubuntu Jenkins agent runs Ansible → Ansible connects to CentOS target → CentOS runs Flask + Node.js + PostgreSQL.

•	Jenkins master: Amazon Linux → runs Jenkins server.

•	Jenkins agent: Ubuntu → builds artifacts (Flask + Node), runs Ansible.

•	Target EC2: CentOS → runs Flask + Node apps + DB installed via Ansible.

---

### Repository Structure

```
dual-app/
├─ flask_app/                  
├─ node_app/                   
├─ db/                         
├─ ansible/
│   ├─ inventories/            
│   │   └─ hosts.ini
│   ├─ playbooks/     
│   │   └─ deploy.yml
│   └─ roles/                  
│       ├─ flask_app/       
│       │   ├─ tasks/main.yml
│       │   └─ templates/flask-app.service.j2      
│       ├─ node_app/        
│       │   └─  tasks/main.yml
│       └─ postgres/     
│           ├─ tasks/main.yml
│           └─  files/schema.sql
├─ jenkins/
│   └─ Jenkinsfile                
├─ ansible.cfg
├─ .gitignore
└─ README.md
```

---

### postgres role workflow:

•  Installs PostgreSQL server + client.

•  Initializes only once (guarded with creates:).

•  Ensures PostgreSQL service is enabled + running.

•  Copies schema.sql to /tmp/schema.sql.

•  Checks if sharedappdb exists.

•  Runs schema.sql 

### flask role workflow:

•  Install Python3 and pip.

•  Copy Flask artifact from the build agent

•  Extract the artifact

•  Create virtual environment and install dependencies

•  Deploy systemd service

•  Start and enable the Flask service

### node role workflow:

•  Install Node.js & npm

•  Copy artifact from jenkins agent

•  Extract artifact

•  Install dependencies

•  Install PM2 globally

•  Start app with PM2

•  Save PM2 process

•  Enable auto-start on reboot

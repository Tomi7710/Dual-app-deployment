## Dual Application Deployment

This project showcases the deployment of a Flask app and a Node.js app with shared database.

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
│       ├─ deploy_flask/       
│       │   ├─ tasks/main.yml
│       │   ├─ handlers/main.yml
│       │   └─ templates/      
│       ├─ deploy_node/        
│       │   ├─ tasks/main.yml
│       │   ├─ handlers/main.yml
│       │   └─ templates/
│       └─ postgres/     
│           ├─ tasks/main.yml
│           ├─ files/schema.sql
│           ├─ handlers/main.yml
│           └─ templates/
├─ jenkins/
│   └─ Jenkinsfile             
├─ scripts/
│   └─ artifact_cleanup.sh     
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

•  Checks if sharedappdb already exists.

•  Runs schema.sql only if the DB is missing.

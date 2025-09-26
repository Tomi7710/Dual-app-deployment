## Dual Application Deployment

This is a Flask app and a Node.js app deployment project.

### Workflow

Ubuntu Jenkins agent runs Ansible → Ansible connects to CentOS target → CentOS runs Flask + Node.js + PostgreSQL.

  Jenkins master: Amazon Linux → runs Jenkins server.

  Jenkins agent: Ubuntu → builds artifacts (Flask + Node), runs Ansible.

  Target EC2: CentOS → runs Flask + Node apps + DB installed via Ansible.

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
│   │   ├─ db.yml      
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
│       └─ postgreSQL/     
│           ├─ tasks/main.yml
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

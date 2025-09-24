## Dual Application Deployment

This is a Flask app and a Node.js app deployment project

---

### Repository Structure
```
project-root/
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
│       └─ setup_postgres/     
│           ├─ tasks/main.yml
│           ├─ handlers/main.yml
│           └─ templates/
├─ jenkins/
│   └─ Jenkinsfile             
├─ scripts/
│   └─ artifact_cleanup.sh     
├─ .gitignore
└─ README.md
```

---

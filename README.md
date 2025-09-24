## Dual Application Deployment

This is a Flask app and a Node.js app deployment project

---

### Repository Structure
```
project-root/
├─ flask_app/                  # Flask app source code
├─ node_app/                   # Node.js app source code
├─ db/                         # Database scripts, schema, seeds
├─ ansible/
│   ├─ inventories/            # Hosts files
│   │   └─ hosts.ini
│   ├─ playbooks/              # Playbooks that call roles
│   │   └─ deploy.yml
│   └─ roles/                  # Ansible roles for deployment
│       ├─ deploy_flask/       # Role to deploy Flask app
│       │   ├─ tasks/main.yml
│       │   ├─ handlers/main.yml
│       │   └─ templates/      # Optional: config templates
│       ├─ deploy_node/        # Role to deploy Node.js app
│       │   ├─ tasks/main.yml
│       │   ├─ handlers/main.yml
│       │   └─ templates/
│       └─ setup_postgres/     # Role to install & configure PostgreSQL
│           ├─ tasks/main.yml
│           ├─ handlers/main.yml
│           └─ templates/
├─ jenkins/
│   └─ Jenkinsfile             # Jenkins pipeline definition
├─ scripts/
│   └─ artifact_cleanup.sh     # Script to remove old builds/artifacts
├─ .gitignore
└─ README.md
```

---

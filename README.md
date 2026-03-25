# devops-interview
devops-interview
# **1) Explain your day-to-day responsibilities**

In my day-to-day role as a DevOps/OpenSearch engineer, I manage **Kubernetes-based applications on AWS EKS**, focusing on **deployment, monitoring, reliability, and security**.

My responsibilities include:

- Managing **EKS clusters**, namespaces, RBAC, and networking
- Deploying and maintaining applications using **Helm charts**
- Managing **OpenSearch clusters** (index management, performance tuning, backups, security)
- Setting up **CI/CD pipelines** for automated deployments
- Monitoring applications using **Prometheus and Grafana**
- Handling **alerts, incidents (INC)**, and **change requests (RFC)** through ITSM tools
- Collaborating with developers, SREs, and QA teams
- Troubleshooting production issues and optimizing performance

# **2) How did you deploy your application on EKS?**

I deploy applications on EKS using a **CI/CD + Helm-based approach**:

1. Infrastructure is provisioned using **Terraform / CloudFormation**
2. Application container images are built using **Docker**
3. Images are pushed to **Amazon ECR**
4. Kubernetes manifests are packaged as **Helm charts**
5. CI/CD pipeline (GitLab/Jenkins) runs:
    - helm lint
    - helm upgrade –install
6. Deployment is validated using:
    - kubectl get pods
    - Health checks
    - Application logs

We use **namespaces** for environment isolation (dev, qa, prod).

# **3) How do you use Helm charts?**

I use Helm charts to:

- Package Kubernetes resources (Deployments, Services, ConfigMaps, Secrets)
- Maintain environment-specific values via values.yaml
- Version applications for easy rollback
- Perform upgrades using helm upgrade
- Roll back using helm rollback

Helm helps us **standardize deployments**, reduce duplication, and manage configuration changes efficiently

# **4) What type of application are you currently handling? Walk me through it**

Currently, I handle **microservices-based applications**, mostly **Java/Spring Boot and Node.js**, deployed on EKS.

Architecture:

- Frontend → API Gateway (Apigee) → Backend microservices
- Logs are sent to **OpenSearch**
- Metrics collected by **Prometheus**
- Dashboards in **Grafana**

Each microservice:

- Runs in its own pod
- Uses ConfigMaps and Secrets
- Communicates internally via Kubernetes Services.

# **5) How do you connect two applications to each other, like DEV and QA connecting internally?**

We use **internal Kubernetes networking**:

- Applications communicate using **ClusterIP Services**
- DNS-based service discovery (service-name.namespace.svc.cluster.local)
- Network access is controlled using **Network Policies**
- Environment separation is ensured using **different namespaces or clusters**

DEV and QA typically do **not directly connect** unless explicitly required and approved.

### **OpenSearch DevOps Engineer Interview Questions & Answers (3–4 Years Experience) | EKS, Helm, Prometheus, Apigee**

# **6) How do you use Prometheus and Grafana?**

- **Prometheus**:
    - Scrapes metrics from Kubernetes and applications
    - Uses exporters (node-exporter, kube-state-metrics)
- **Grafana**:
    - Visualizes metrics using dashboards
    - Displays CPU, memory, pod health, latency, error rates

We use Grafana dashboards for **capacity planning and troubleshooting**.

# **7) Have you set up or configured any alerts?**

Yes, I have configured alerts using **Prometheus Alertmanager**:

- High CPU/Memory usage
- Pod crash loops
- Node failures
- OpenSearch cluster health issues

Alerts are integrated with **email, MS Teams, and ITSM tools** for incident creation.

# **8) How do you handle deployments?**

We follow a **CI/CD-driven deployment strategy**:

- Feature branches → DEV
- Approved builds → QA
- Production deployments require **RFC approval**
- Use **rolling updates** or **blue-green deployments**
- Rollbacks are handled via Helm

Post-deployment checks include logs, metrics, and health endpoints.

# **9) How do you use ITSM services like RFC and INC?**

- **RFC (Request for Change)**:
    - Raised for production changes
    - Includes risk, rollback plan, and schedule
- **INC (Incident)**:
    - Created for production issues
    - Severity-based escalation
    - Root Cause Analysis (RCA) after resolution

This ensures compliance and audit readiness.

# **10) How do you keep yourself updated regarding Helm charts?**

I stay updated by:

- Following **Helm GitHub releases**
- Reading Kubernetes and CNCF blogs
- Testing new Helm features in DEV
- Reviewing official Helm documentation
- Learning from real deployment issues and improvements

# **11) Explain APIGEE proxy: how is it configured and set up?**

Apigee Proxy acts as an **API gateway**:

- Routes external traffic to backend services
- Handles authentication, rate limiting, logging
- Configured using:
    - Proxy endpoints
    - Target endpoints
    - Policies (OAuth, spike arrest, quotas)
- Integrated with Kubernetes services internally

It provides **security, monitoring, and traffic control**.

# **12) If something changes in a Helm chart, how do you track it and install it on Kubernetes?**

- Helm charts are stored in **Git repositories**
- Changes are tracked via **Git commits**
- CI pipeline detects changes
- Run:
- helm diff upgrade
- helm upgrade –install
- Version bump is mandatory
- Changes are tested in lower environments before prod

# **13) With whom do you collaborate? How do you work together?**

I collaborate with:

- **Developers**: app configs, troubleshooting
- **QA teams**: environment readiness
- **SRE teams**: reliability and scaling
- **Security teams**: compliance and access control

We use **Agile ceremonies, Jira, and Slack/Teams** for coordination.


##FAQ
**1️⃣ What are the core responsibilities of an OpenSearch DevOps Engineer?**

An OpenSearch DevOps Engineer is responsible for deploying, managing, monitoring, and optimizing OpenSearch clusters. This includes infrastructure automation, Kubernetes deployments, CI/CD pipelines, monitoring with Prometheus and Grafana, ensuring high availability, security, and performance tuning while collaborating closely with development and SRE teams.

**2️⃣ How is OpenSearch deployed on AWS EKS?**

OpenSearch is typically deployed on EKS using Helm charts or Kubernetes manifests. The setup includes StatefulSets, persistent volumes, ConfigMaps, Secrets, and services. Load balancers or ingress controllers expose the service, while IAM roles, node groups, and autoscaling ensure reliability and scalability.

**3️⃣ Why are Helm charts important in DevOps workflows?**

Helm charts help package, version, and deploy Kubernetes applications efficiently. They enable parameterized deployments using values files, simplify rollbacks, and ensure consistency across environments like DEV, QA, and PROD.

**4️⃣ How do DevOps engineers monitor OpenSearch and applications?**

Monitoring is done using Prometheus for metrics collection and Grafana for visualization. Metrics include JVM memory, cluster health, node status, CPU usage, and indexing/search latency. Alerts are configured to notify teams about performance or availability issues.

**5️⃣ How do you configure alerts in a DevOps environment?**

Alerts are set using Prometheus Alertmanager or Grafana alerting rules. Common alerts include pod crashes, high memory usage, disk space exhaustion, node unavailability, and API latency thresholds. Alerts are integrated with email, Slack, or ITSM tools.

**6️⃣ How do different environments (DEV, QA, PROD) communicate internally?**

Internal communication between environments is handled using Kubernetes Services, internal load balancers, private DNS, or service mesh tools. Network policies and security groups ensure secure and controlled access.

**7️⃣ How are deployments handled in Kubernetes?**

Deployments are managed using CI/CD pipelines that trigger Helm upgrades or Kubernetes rollouts. Strategies such as rolling updates, blue-green, or canary deployments are used to ensure zero downtime and controlled releases.

**8️⃣ What role does ITSM (RFC, INC) play in DevOps?**

ITSM processes ensure governance and traceability. RFCs (Request for Change) are raised for planned changes like deployments or upgrades, while INCs (Incidents) are logged for production issues. DevOps teams work closely with support teams to resolve incidents efficiently.

**9️⃣ How is an application exposed to external users?**

Applications are exposed using Kubernetes Services such as LoadBalancer or Ingress resources. In enterprise environments, API gateways like Apigee are used to manage traffic, security, rate limiting, and API lifecycle management.

**How do you stay updated with DevOps tools like Helm and Kubernetes?**

DevOps engineers stay updated by following official documentation, GitHub repositories, release notes, blogs, webinars, community forums, and hands-on labs. Continuous learning and certifications also help stay current with evolving technologies.
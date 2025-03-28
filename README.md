# ARISA-MLOps
## Sessions 01 and 02 - Questions Answers

---

**1. Why is MLFlow useful?**

MLFlow is very useful in the ML lifecycle because it allows us to track experiments, log metrics, and store artifacts (such as models and plots). This makes it easier to compare different runs and select the best performing model. It also helps with reproducibility by saving all details like code versions, hyperparameters, and data inputs, and it supports model versioning and collaboration among team members.

---

**2. What is the purpose of having automated pipelines in an ML production environment? Why can't a data scientist just run notebooks to train models and produce predictions?**

Automated pipelines are essential for several reasons:
- **Consistency and Reproducibility:** They ensure that every training or prediction run follows the same process, reducing human errors that can occur when running notebooks manually.
- **Scalability:** Automated pipelines can be scheduled, monitored, and scaled, which is crucial when models need to be updated or retrained continuously.
- **CI/CD Integration:** They integrate well with Continuous Integration/Continuous Deployment practices, enabling smoother and faster deployments with less downtime.
- **Auditing and Logging:** They provide clear logs and audit trails for each run, making it easier to troubleshoot and verify the processes.

Notebooks are great for exploration, but they lack the robustness and scalability needed for production systems.

---

**3. What is the difference between A/B testing, Green/Blue deployments, Canary deployments, and Challenger/Champion deployments?**

- **A/B Testing:**  
  Two or more versions of a model run concurrently with a split of the traffic between them. This method collects performance data from real users, allowing us to statistically compare the models.

- **Green/Blue Deployments:**  
  Two identical production environments are maintained (blue for the current version and green for the new version). The new version is deployed to the idle (green) environment, and once verified, the traffic is switched over from blue to green. This minimizes downtime and facilitates quick rollback if needed.

- **Canary Deployments:**  
  A new model is released to a small subset of users initially. This gradual rollout helps in identifying any potential issues early on, before rolling out the model to the entire user base.

- **Challenger/Champion Deployments:**  
  The current model (champion) is compared with a new model (challenger) running in parallel. The challenger only replaces the champion if it outperforms it, ensuring that the best-performing model is used in production.

---

**4. Why are we hosting artifacts in AWS S3 and metadata in RDS?**

The decision to host artifacts in AWS S3 and metadata in RDS is based on the strengths of each service:
- **AWS S3:**  
  S3 is ideal for storing large, unstructured data such as models, logs, and datasets. It offers high scalability, durability, and cost-efficiency.
- **RDS:**  
  RDS, typically using PostgreSQL in our case, is better suited for structured data like experiment parameters and metrics. It provides reliable query capabilities and transactional integrity, which are important for managing metadata effectively.

---

**5. What are some security concerns and challenges involved with using secrets and API keys to authenticate our GitHub Actions workflow instance?**

There are several security challenges:
- **Risk of Exposure:**  
  If secrets (such as AWS keys or the Kaggle API key) are not handled carefully, they might be accidentally exposed in logs or through misconfigurations, leading to unauthorized access.
- **Access Control:**  
  It is important to ensure that these secrets have only the minimal permissions required. Over-privileging increases the potential damage in case of a leak.
- **Secret Rotation and Management:**  
  Regularly updating and rotating these keys is critical to minimize the risk period if a key is compromised.
- **Environment Protection:**  
  Ensuring that the secrets are not printed or stored in an insecure manner during the build and deployment process is another key challenge.

---

**6. What was the biggest challenge for you in completing the assignment?**

For me, the biggest challenge was setting up and integrating the entire MLOps pipeline. This included:
- **Infrastructure Configuration:**  
  Correctly setting up AWS services (S3 for artifacts and RDS for metadata) and ensuring they worked seamlessly with the MLFlow tracking server.
- **Pipeline Automation:**  
  Moving from exploratory notebooks to fully automated pipelines in GitHub Actions required a good understanding of CI/CD practices and handling various dependencies.
- **Security Concerns:**  
  Ensuring that secrets and API keys were managed securely and not accidentally exposed in the workflow added an extra layer of complexity.

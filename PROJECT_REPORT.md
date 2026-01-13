**CI/CD DevSecOps Pipeline for Python Library Management System**

**1. Project Title**
      Automated CI/CD DevSecOps Pipeline for Containerized Python Library Application Using Jenkins, Docker, SonarQube, Trivy & Docker stack.      

**2. Project Objective**
	The objective of this project is to design and implement a secure, automated CI/CD pipeline that:
        * Automates  : code pulling from GitHub based on branch selection.
        * Performs   : deep code quality analysis to identify bugs and security hotspots.
        * Builds     : containerized microservices using Docker stack.
        * Scans      : Docker images for vulnerabilities before deployment.
        * Enforces   : a manual approval gate for production safety.
        * Deploys    : the application stack using a single command.
        * Notifies   : stakeholders of build results via automated emails.

**3. Technologies Used**

	| Category         | Tools                              |
	| ---------------- | ---------------------------------- |
	| Source Control   | GitHub                             |
	| CI/CD            | Jenkins                            |
	| Code Quality     | SonarQube                          |
	| Containerization | Docker, Docker Stack               |
	| Security         | Trivy (Image scanning)             |
	| Deployment       | Docker Stack                       |
	| Notifications    | Jenkins Email                      |
	| Application      | Python Microservices (Library App) |

**4. Application Overview**
	The system is built using a modern microservices architecture:
        * Frontend Service       	:  User interface for the library app.
        * Authentication Service    :  Manages user login and security.
        * Book Service        		:  Handles book inventory management.
        * Borrow Service        	:  Manages the lending and returning logic.
        * Database Service       	:  Persistent storage using MySQL 8.0.

**5. CI/CD Pipeline Architecture**

		Developer → GitHub → Jenkins Pipeline → SonarQube
													↓
                         Docker Build (Stack)    
                                ↓
                           Trivy Scan
                                ↓
                           Image Tagging
                                ↓
                       Approval Gate (RM)
                                ↓
                        Docker Stack Deploy
                                ↓
                        Email Notification

**6. Pipeline Workflow Explanation**

	Stage 1: Source Code Checkout
		Jenkins pulls the code from the specified GitHub branch (`master`, `main`) using parameterized inputs.

	Stage 2: Code Quality Analysis (CQA)
		SonarQube scans the Python source code for Bugs, Vulnerabilities, and Code Smells. This ensures only high-quality code proceeds to the build stage.

	Stage 3: Docker Image Build
		Instead of building images locally, Jenkins pulls pre-built, versioned images from DockerHub:
			* dattasai1999/digital_lib:db
			* dattasai1999/digital_lib:auth
			* dattasai1999/digital_lib:book
			* dattasai1999/digital_lib:borrow
			* dattasai1999/digital_lib:frontend

	Stage 4: Security Scan (Trivy)
		All built images are scanned for vulnerabilities. The pipeline is configured to fail (`exit-code 1`) if any "HIGH"or"CRITICAL" issues are detected.

	Stage 5: Image Tagging
		Standardizes local images by tagging them with the DockerHub repository name (`dattasai1999/digital_lib`).

	Stage 6: Manual Approval
		A blocking step that requires a Release Manager (RM) to manually approve the transition from "Build/Scan" to "Deployment."

	Stage 7: Deployment
		Executes `docker stack deploy -c docker-compose.yml my_lib' the microservices container stack on the target environment.

	Stage 8: Email Notification
		Sends an automated email containing the Build Status, Job Name, and a direct link to the execution logs.

**7. Security & Quality Controls**

	| Layer              | Tool                  |
	| ------------------ | --------------------- |
	| Code Security      | SonarQube             |
	| Image Security     | Trivy                 |
	| Approval           | Manual Gate           |
	| Build Integrity    | Jenkins               |
	| Container Security | Docker Best Practices |

**8. Key Features**

	* Branch-based deployment
	* Automated code quality checks
	* Dockerized microservices
	* Vulnerability scanning
	* Manual release approval
	* Zero-downtime deployment
	* Email notifications

**9. Conclusion**
	This project demonstrates a production-grade DevSecOps pipeline. By integrating security tools like Trivy and SonarQube directly into the Jenkins workflow, the "Shift-Left" security approach is achieved.

## 📸 Proof of Concept

### Pipeline Execution
![Jenkins Pipeline Status](./screenshots/jenkins_img.png)

### Video Demonstration
[Click here to watch the deployment process](./screenshots/app_proof.mp4)
  resulting in a more resilient and reliable software delivery process.






# DIPLOMA PROJECT REQUIREMENTS DOCUMENT

---

## 1. Project Objective

Design and implement a scalable, distributed, web-based infrastructure that ingests real-time domain-specific data streams, processes the data for anomaly detection or trend analysis, generates predictive forecasts, and visualizes the results for end-users.

## 2. Business Rules & Domain Logic

Students must analyze their specific domain and define concrete business rules for both data and processes.

## 3. Functional Requirements (FR)
* **FR1: Data Ingestion:** The system must accept continuous streams of domain-specific data (via simulated generators, public APIs, or mock IoT devices).
* **FR2: Event Streaming:** All incoming data must be routed through a message broker (Apache Kafka) to ensure decoupling, buffering, and scalability.
* **FR3: Analytics Processing:** The Python module must consume data from Kafka, apply domain-specific analytical/ML algorithms, and publish processed results back to the broker or directly to the database.
* **FR4: User Management:** The backend must support Role-Based Access Control (RBAC) for at least three roles: *Administrator*, *Domain Analyst/Expert*, and *Standard/Public User*.
* **FR5: Interactive Dashboard:** The frontend must display real-time data visualizations, historical trend charts, map/spatial representations (if applicable), and forecasting gauges.
* **FR6: Alerting & Reporting System:** The system must generate, store, and allow users to query historical alerts and generate summary reports based on the Business Rules.

## 4. Non-Functional Requirements (NFR)
* **Scalability:** The architecture must be horizontally scalable. Adding more instances of the Backend API or Python Analytics workers must automatically increase processing throughput.
* **Performance:** The frontend dashboard must reflect new processed data/events with a latency of no more than 3–5 seconds from the moment they enter the Kafka topic.
* **Reliability:** The system must handle message broker or database downtime gracefully without losing unprocessed messages (utilizing proper Kafka acknowledgment, offset management, and retries).
* **Extensibility:** Services should be modular, allowing new analytical models or algorithms to be swapped in or added without altering the core ingestion pipeline.

## 5. Technology Stack & Architecture Constraints
Students must adhere to the following technology constraints:

### 5.1. Allowed Technologies
* **Frontend:** Free choice (React, Vue, Angular, Svelte, etc.). Must include interactive data visualization and mapping/charting libraries.
* **Backend API:** Spring Boot (Java), Node.js (NestJS/Express), or PHP based frameworks. *Responsible for REST APIs, Authentication, User Management, and serving the frontend.*
* **Data Analytics Module:** **Pure Python** (No heavy web frameworks like Django/FastAPI for this specific module). Use standard data/ML libraries (Pandas, NumPy, Scikit-learn, PyTorch, etc.) and Kafka consumer libraries (`confluent-kafka` or `kafka-python`). This module acts purely as background processing workers.
* **Message Broker:** **Apache Kafka** (Mandatory). Acts as the central nervous system for inter-module communication.
* **Databases:**
    * Relational or NoSQL (PostgreSQL, MongoDB, MySQL etc.)
* Alternative Platforms: If a group wishes to employ an alternative platform, they must discuss and clear it with the project 
supervisor beforehand.
  
### 5.2. Architectural Flow
1. **Ingestion Service** (can be a simple script or part of the backend) pushes raw data to a Kafka Topic (e.g., `raw-domain-data`).
2. **Python Analytics Workers** consume from the raw topic, process the data using domain logic, and publish results to output topics (e.g., `processed-events`, `forecast-results`) or write directly to the database.
3. **Backend API** consumes from the processed topics (or reads from the DB) to serve data to the frontend via REST or WebSockets.
4. **Frontend** polls or uses WebSockets to display real-time updates.

## 6. Design Deliverables (UML & ER Diagrams)
Before coding, students must submit a System Design Document containing the following diagrams:

### 6.1. UML Diagrams
1. **Use Case Diagram:** Illustrate interactions between Actors (Standard User, Domain Analyst, Admin, System Timer) and system capabilities.
2. **Class Diagram:** Detail the core domain models for both the Backend and the Python module. Show relationships, attributes, and key methods.
3. **Sequence Diagram:** Map the exact lifecycle of a single data event from Ingestion $\rightarrow$ Kafka $\rightarrow$ Python Processing $\rightarrow$ Database $\rightarrow$ Frontend display.
4. **Component/Deployment Diagram:** Show the logical deployment. Must explicitly demonstrate **scalability** (e.g., multiple Kafka partitions, multiple Python consumer groups, load balancers for the Backend).

### 6.2. Entity-Relationship (ER) Diagram
Design the database schema. It should include entities like:
* **Users & Roles** (Authentication/Authorization)
* **Data Sources/Sensors** (Metadata about where the data is coming from)
* **Core Domain Events** (The raw or processed data records, heavily indexed by time)
* **Anomalies/Alerts** (Linked to Core Events, including severity and status)
* **Forecasts/Predictions** (Time windows, confidence scores, regions/categories)
* *Note: Students must justify their choice of database(s) and explain how they will handle time-series data partitioning and indexing.*

## 7. Project Schedule & Timetable
*Students are required to create a detailed project schedule (e.g., using a Gantt chart or a detailed weekly breakdown) 
tailored to their specific team size and topic complexity. This schedule must be submitted during Phase 1.*

**Below is an EXAMPLE timetable to guide your planning. You must adapt this to your specific project context.**

### *Example Timetable (16-Week Semester)*
| Phase | Week | Milestone / Focus Area | Key Deliverables for the Week |
| :--- | :--- | :--- | :--- |
| **1** | 1-2 | **Requirements & Domain Analysis** | Finalize business rules, define data sources, draft initial ER/UML. |
| | 3 | **System Design Sign-off** | Submit finalized UML, ER diagrams, and Tech Stack justification. |
| **2** | 4-5 | **Infrastructure & Backend Setup** | Kafka cluster setup, Backend API skeleton, Database schema creation. |
| | 6 | **Backend Core Features** | Implement Auth (RBAC), basic CRUD APIs, and data ingestion endpoints. |
| **3** | 7-8 | **Analytics Module Development** | Python Kafka consumers setup, implement core data processing logic. |
| | 9-10 | **Advanced Analytics & Integration** | Implement forecasting/anomaly algorithms, connect Python output to DB/Kafka. |
| **4** | 11-12 | **Frontend Development** | UI layout, interactive charts/maps, connect to Backend APIs/WebSockets. |
| | 13 | **End-to-End Integration** | Full data flow working from ingestion to frontend display. |
| **5** | 14 | **Testing & Optimization** | Unit/Integration testing, fixing bugs, optimizing database queries. |
| | 15 | **Scalability & Load Testing** | Run multiple Python/Backend instances, perform load testing, document results. |
| **6** | 16 | **Finalization & Defense** | Final code cleanup, documentation, presentation preparation, Final Defense. |

## 8. Diploma Project Report (Thesis) Requirements
At the conclusion of the project, students must submit a comprehensive, professionally formatted report. This document 
serves as the official academic record of the project and must clearly articulate the engineering decisions 
made throughout the development lifecycle.

### 8.1. Required Structure
The report book must include the following chapters:
1. **Introduction:** Project background, problem statement, objectives, scope, and the structure of the report.
2. **Literature Review & Domain Analysis:** Context of the specific domain, analysis of existing solutions, and justification for the chosen approach.
3. **System Requirements & Design:** Detailed business rules, functional/non-functional requirements, and the required UML (Use Case, Class, Sequence, Component/Deployment) and ER diagrams.
4. **Implementation & Architecture:** Detailed explanation of the technology stack, Kafka configuration (topics, partitions, consumer groups), Backend API design, and the Pure Python analytics logic. Include key architectural decisions and essential code snippets (do not paste entire codebases).
5. **Conclusion & Future Work:** Summary of achievements, limitations encountered, and recommendations for future enhancements.
6. **References & Appendices:** Academic citations (IEEE/APA format), user manuals, and deployment/setup instructions.

### 8.2. Formatting & Submission Guidelines
* **Format:** PDF format, strictly adhering to the university's official thesis template and formatting guidelines.
* **Length:** Typically between 40 to 70 pages (excluding appendices and references).
* **Originality:** The report must pass a plagiarism check (e.g., Turnitin) with a similarity index below the university's threshold (usually < 15-20%). Code snippets and standard boilerplate are generally excluded from this check.
* **Submission:** TBA

## 9. Evaluation Criteria
The project will be graded based on the following rubric:
1. **Architecture & Scalability (20%):** Proper use of Kafka and decoupled microservices.
2. **Domain Logic & Analytics (20%):** Correct implementation of the defined business rules, quality and accuracy of the Python analytics/forecasting logic.
3. **Software Design & UML (15%):** Clarity, accuracy, and completeness of UML and ER diagrams.
4. **Implementation Quality (15%):** Clean code, proper error handling, logging, and strict separation of concerns across Frontend, Backend, and Python modules.
5. **UI/UX & Presentation (15%):** Intuitive frontend design, effective data visualization, project management (adherence to schedule), and quality of the final defense presentation.
6. **Diploma Project Report (15%):** Quality, structure, and professionalism of the report. This includes adherence to 
formatting guidelines, clarity of technical explanations, originality (plagiarism check), and comprehensive coverage of requirements, design, implementation, and testing phases.

---
**Instructor Notes / Tips for Students:**
* *Data Sources:* If real-time domain data is unavailable, you must write a robust "Data Generator" script (in Python or Node) that simulates realistic, high-velocity data streams based on historical distributions or statistical models.
* *Kafka Implementation:* Do not just use Kafka as a simple message queue. Utilize Kafka Topics, Partitions, and Consumer Groups to prove your system can scale horizontally.
* *Python Module:* Since the Python module is "pure", focus on writing robust, standalone worker scripts. To achieve scalability, you should be able to run multiple instances of your Python script simultaneously, utilizing Kafka Consumer Groups to distribute the workload.
* *Project Management:* Stick to your proposed timetable. If you fall behind, communicate with your supervisor immediately to adjust the scope rather than compromising on code quality.


---

### By adhering to these guidelines and policies, you will ensure that your submission is complete and meets the evaluation criteria.

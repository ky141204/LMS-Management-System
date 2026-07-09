---
title: "Event 2"
date: 2026-05-23
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# REFLECTION: AWS COMMUNITY DAY VIETNAM TECHNOLOGY SEMINAR

---

> [!IMPORTANT]
> ### 📅 Event overview and goal
> **AWS Community Day Vietnam 2026** is the largest community technology event of the year for the Amazon Web Services cloud computing ecosystem. This reflection summarizes and analyzes insights from **6 practical sessions** around today's hottest trends: the AWS ecosystem, Generative AI, enterprise Multi-Agent architecture, and cloud cost and performance optimization strategies.

## 1. DETAILED CONTENT OF THE REFLECTIONS

### Event participation information
* **Format:** Offline.
* **Attendance location:** 26th floor.
* **Attendance time:** 9:00 AM.

### Session 1: Making AI Actually Work for You — Context Is Everything

* **Speaker:** Trịnh Trường (Tinh Truong) - Platform Engineer at GoTymeX.
* **Main topic:** The importance of context in optimizing AI effectiveness and building a "Second AI Brain".

#### Core content:

1. **The bottleneck in AI applications:**
   * Many AI results fail to meet expectations not because the model is weak, but because the input context is missing, such as vague prompts, missing target information, or missing constraints.
   * AI cannot read the user's mind; it only works based on what is provided.
2. **Definition of context:** Context includes Goal, real-world Situation, technical/budget/format Constraints, and related Evidence.
3. **Common mistakes when providing context:**
   * *Internet Puller:* Copying entire long documents or many screenshots into a chatbot makes the model noisy and increases token cost.
   * *Repeating what AI already knows:* For example, providing Express.js code and asking AI to write in Express.js again instead of specifying the exact refactor requirements such as pagination or validation.
   * *Missing goals and constraints.*
4. **Evolution of AI applications:** From **Prompt (single question)** $\rightarrow$ **Context (context-aware system)** $\rightarrow$ **Memory (personalized memory system)**.
5. **"Second AI Brain" model:**
   * Operates in a cycle: **Store (notes/code)** $\rightarrow$ **Retrieve (relevant parts)** $\rightarrow$ **Generate (answer)** $\rightarrow$ **Learn (remember lessons)**.
   * Maps to AWS services: Amazon S3, Vector DB, Amazon Bedrock, and observability tools.

---

### Session 2: Friendly AI Assistant with Amazon Q (Quick)

* **Speaker:** Phạm Ngô Hải Anh - AWS Community Builder at G-AsiaPacific Vietnam.
* **Main topic:** Building a friendly enterprise AI assistant using Amazon Quick (Amazon Q) solution suite.

#### Core content:

1. **Pain points of enterprise users:** Spending too much time collecting/analyzing information from many sources, performing repetitive tasks, and depending on experts for in-depth data analysis.
2. **AWS Agentic AI solution:**
   * Introduced **Amazon Quick Suite** - a unified experience that securely integrates enterprise data to shorten the path from data to action.
   * Strong connectivity: more than 40 data connectors, support for user-uploaded data, databases, and large data warehouses.
3. **Governance and security framework (Responsible AI):** Ensures safety through access controls, guardrails, and legal compliance.
4. **Practical use case:** Project Management Assistant that automates Minutes of Meeting (MoM), sends emails to stakeholders, and automatically schedules the next meeting.

---

### Session 3: From Edge to Origin — CloudFront as Your Foundation

* **Speaker:** Nguyễn Tuấn Thịnh - DevOps Engineer at First Cloud AI Journey.
* **Main topic:** Optimizing cost, security, reliability, and web infrastructure performance through Amazon CloudFront.

#### Core content:

1. **Customer challenge with traditional CDN cost:**
   * Pay-as-you-go traffic pricing can create "bill spike" risks of hundreds of thousands of USD during sudden traffic surges or DDoS attacks.
2. **New solution from AWS (launched November 2025):**
   * Fixed-Price CDN & Security Pricing Plans include CDN (CloudFront), WAF, DDoS protection, DNS (Route 53), Logging (CloudWatch), and S3 storage. This helps businesses forecast monthly costs proactively.
3. **Distributed Denial of Service (DDoS) protection:** Uses CloudFront's global distributed network architecture (700+ PoPs in 50+ countries) together with AWS Shield and AWS WAF to block malicious traffic at edge locations closest to the attack source.
4. **Cost and performance optimization:**
   * Free Data Transfer Out (DTO) from AWS origin services to CloudFront.
   * Reduces CPU load on origin servers (EC2/ALB) by moving TLS handshake (HTTPS), compression (Gzip/Brotli), and static delivery to CloudFront.
   * Improves performance through multi-layer caching (Edge $\rightarrow$ Regional Edge Caches $\rightarrow$ Origin Shield) and HTTP/3 (QUIC/UDP), which supports superior parallel loading compared with HTTP/1.1.
5. **Advanced security mechanisms:**
   * Supports Mutual TLS (mTLS), Origin Access Control (OAC) to hide origin servers (S3, API Gateway, Lambda), and Signed URL/Signed Cookies to protect copyrighted digital content.

---

### Session 4: 36 Hours with LotusHacks — Building UTMorpho from Idea to Reality

* **Speaker/Team:** Team VIB.
* **Main topic:** Practical experience at Vietnam's largest hackathon (LotusHacks) and the journey of building UTMorpho in 36 hours.

#### Core content:

1. **Journey from zero:** Starting with no concrete idea (Hour 0), the team found inspiration from direct pain points in daily work to create **UTMorpho**, a tool focused on optimizing content editing experience.
2. **Development process under time pressure (36 hours):**
   * Setup and team alignment.
   * Build the core slice first.
   * Overcome the hard middle stage of the project.
   * Integrate, polish, and prepare the pitch.
3. **Technical challenges and failures:**
   * AI generated too much unnecessary content (AI Overgeneration).
   * Model token limits.
   * Fatigue and burnout near presentation time.
4. **Hard-earned lessons:**
   * "Real Frustration Creates Real Ideas."
   * Many ideas are not as valuable as one high-quality and focused idea.
   * Communication and team synchronization determine success or failure under time pressure.

---

### Session 5: Non-Determinism of "Deterministic" LLM Settings

* **Speaker:** Đức Đào (Duc Dao) - Solution Architect at Cloud Kinetics.
* **Main topic:** The non-deterministic nature of LLMs even when Temperature = 0, and mitigation strategies.

#### Core content:

1. **Theory vs. reality:**
   * *Theory:* When `Temperature = 0`, the model activates greedy decoding, always choosing the token with the highest probability at each step to ensure deterministic output.
   * *Reality:* Experimental research across 5 large models (GPT-3.5, GPT-4o, Llama-3, Mixtral) shows that **no model achieves absolute stability**. Answer accuracy can vary by up to 15% between identical runs, and exact string match (TARr@10) is almost 0% for difficult tasks.
2. **Core causes:**
   * *Technical cause (GPU):* Floating-point arithmetic on GPUs is not associative (`(a + b) + c` is not always equal to `a + (b + c)` under IEEE 754). Non-deterministic parallel execution order on GPUs creates tiny rounding errors in logits, which can change the token selected by argmax.
   * *Commercial cause (Batching):* API providers batch many requests from different users into one inference run to optimize hardware cost. The computation for your request can be affected by other parallel requests in the same batch.
3. **Mitigation strategies:**
   * *Multiple runs and majority voting:* Run the prompt several times and use the most common result.
   * *Structured output constraints:* Use JSON mode or function calling to narrow the possible output vocabulary.
   * *Self-host the model:* Control the entire inference infrastructure parameters.
   * *Practical tip:* Set `Temperature = 0.1` instead of `0` to avoid repetitive loops, while designing downstream systems to handle information variance.

---

### Session 6: Enterprise-Grade Multi-Agent System — The Case of Startup Credit Scoring

* **Speaker:** Vy Lâm (Vy Lam) - Senior Business Systems Analyst at VPBank.
* **Main topic:** Designing an enterprise-grade Multi-Agent system to solve the startup credit scoring problem.

#### Core content:

1. **Structural mismatch:** Traditional banking credit scoring relies on collateral, 3-year financial statements, and long-term credit history. Startups only have 6-18 months of operation, assets mainly consisting of intellectual property (IP), team capability, traction metrics, and mostly unstructured data.
2. **Limitations of Single Agent:** Expertise can become diluted due to overly broad context limits, no checks and balances mechanism, and unreliable outputs.
3. **Virtual Credit Committee (Multi-Agent) model:**
   * Specialized agents cooperate closely: **Financial Analyst** (cash flow, burn rate), **Market Analyst** (TAM/SAM/SOM, competitors), **Team Evaluator** (founder capability), **Risk Assessor** (risk evaluation), and **Compliance Agent** (banking policy compliance).
   * Agents are coordinated by a **Manager Agent** to produce a consensus credit score with a clear audit trail.
4. **6 pillars of Enterprise-Grade AI:** Security, Data Governance, Network (isolated VPC), Operations, Human Factors, and Compliance.
5. **Return on investment (real ROI):**
   * Reduces application processing time from **2-3 weeks to 2-4 hours** (95% faster).
   * Reduces specialist working hours from **40-60 hours to 2-4 hours**.
   * Increases approval rate from **15-20% to 35-45%** by correctly understanding startup data.
   * Reduces decision-making cost by 95%.
6. **Implementation roadmap:** Goes through 4 phases: **Foundation** $\rightarrow$ **Integration** $\rightarrow$ **Pilot** $\rightarrow$ **Scale**.

---

## 2. Deep Analysis of the Technology Trends

### 2.1. Context Engineering becomes a core AI skill

One theme across the sessions is that AI should no longer be treated as a tool where users simply ask a question and receive an answer. To get useful results, users need to provide complete, clear, and focused context.

In practice, many students or junior developers use AI with very short prompts such as "write a login API" or "fix this code." This may produce quick output, but the result is often unstable because the model does not understand the project framework, security requirements, input data, or completion criteria.

From the **Context Is Everything** session, I learned that a good prompt should include:

* **Clear goal:** what output is expected.
* **System context:** what technologies and architecture the project uses.
* **Constraints:** time, budget, coding style, and output format.
* **Evidence:** logs, code snippets, screenshots, or related documents.
* **Evaluation criteria:** how to decide whether the result is correct and usable.

This skill is close to how software engineers work in real organizations: before implementation, they need to understand requirements, business context, and technical constraints. AI amplifies user capability only when the user can frame the problem properly.

### 2.2. Cloud infrastructure is the foundation of modern AI applications

The sessions showed that AI cannot be separated from cloud infrastructure. A real AI application needs more than a large language model. It needs storage, knowledge retrieval, security, monitoring, APIs, CDN, databases, and operational pipelines.

For example, to build an internal AI assistant, an organization may need to:

* Store documents in S3 or an equivalent storage system.
* Create a vector index for relevant retrieval.
* Use Bedrock or another model platform to generate responses.
* Control access based on roles.
* Log activity, monitor cost, and detect errors.
* Protect endpoints with WAF, CDN, or authentication.

This helped me realize that learning AI is not only about prompts or models. To bring AI into real products, learners need to understand cloud architecture, security, networking, and observability.

### 2.3. Cost optimization is an engineering problem, not only a financial problem

The CloudFront session showed that cloud costs can grow quickly if the system is not designed properly. For web or AI applications with many users, traffic, API requests, and data transfer can become major cost drivers.

Cost optimization does not mean always choosing the cheapest service. The key is choosing the right architecture:

* Use CDN to reduce origin load.
* Cache static and frequently accessed content.
* Set billing alerts early.
* Monitor abnormal request patterns.
* Choose the right compute model for each workload.
* Stop or clean up unused resources.

For students, this lesson is very practical. When building projects on AWS, forgetting EC2, NAT Gateway, databases, or load balancers can create unexpected costs. Therefore, reading pricing pages, setting budgets, and cleaning up resources are important parts of cloud learning.

### 2.4. Multi-Agent systems introduce a more advanced AI design direction

The Multi-Agent session showed that a single agent struggles with large business workflows, especially problems that require multiple perspectives such as finance, credit scoring, project management, or customer support.

A Multi-Agent model divides the system into specialized agents:

* Financial analysis agent.
* Risk assessment agent.
* Compliance checking agent.
* Result summarization agent.
* Workflow coordination agent.

The benefit is that each agent has a clearer scope, reducing overly broad context and improving verification. However, Multi-Agent systems also introduce new challenges: synchronizing state, avoiding contradictory answers, controlling access, and maintaining audit trails.

---

## 3. Connection to Student Learning and Projects

### 3.1. Applying the lessons to personal projects

After the event, I can apply these lessons to personal projects in a more practical way. For example, if I build a student event management website, I can:

* Use CloudFront to distribute the static frontend.
* Use API Gateway and Lambda for the backend.
* Use DynamoDB to store registration information.
* Use IAM roles with minimum permissions.
* Use CloudWatch for logs and error monitoring.
* Use an AI assistant to support event information lookup, while keeping context and source data clear.

This means the lessons from AWS Community Day are not only theoretical; they can directly influence concrete project design.

### 3.2. Changing how I use AI for learning

Previously, many learners used AI as a quick-answer tool. After the event, I realized that AI should be used as a more structured learning partner:

* Ask AI to explain concepts, but verify with official documentation.
* Use AI to review code, but still understand the errors myself.
* Use AI to create deployment checklists.
* Use AI to compare architecture options.
* Avoid copying AI output into a project without checking it.

Especially when using AI for code, I need to provide enough context: technology stack, related files, specific errors, expected output, and boundaries for allowed changes.

### 3.3. Building an operations mindset

Another important point is that the sessions were not only about building applications, but also about operating them. In real environments, a good system is not only one that "runs." It must also be:

* Observable.
* Secure.
* Scalable.
* Cost-aware.
* Debuggable through logs.
* Recoverable through rollback procedures.

This is the difference between a demo project and a real product. For students, developing an operations mindset early will make internships and real work easier to adapt to.

---

## 4. Action Plan After the Event

After joining AWS Community Day Vietnam, I set several concrete directions:

1. **Review AWS fundamentals:** IAM, S3, EC2, VPC, Lambda, CloudWatch, and CloudFront.
2. **Build a mini cloud project:** deploy frontend, backend, database, and monitoring.
3. **Practice context engineering:** write prompts with goals, context, constraints, and evaluation criteria.
4. **Learn more about RAG:** store documents, create embeddings, and retrieve relevant information.
5. **Monitor cloud cost:** set budget alarms and clean up resources after practice.
6. **Explore Multi-Agent design:** try designing a simple multi-agent system, such as a requirement analysis agent, bug checking agent, and summarization agent.
7. **Document lessons learned:** keep notes about errors, fixes, and deployment experiences.

This plan turns the event knowledge into concrete actions. The greatest value of the event is that it expanded my perspective: modern technology is not one isolated tool, but a combination of AI, cloud, security, operations, and product thinking.

---

> [!TIP]
> ### 💡 Lessons and general awareness (Synthesis)
>
> From the presentations above, three major trend-level lessons can be drawn about applying technology today:
>
> 1. **The shift from "simple AI" to "compound and specialized AI systems"**:
>    * Basic prompting has reached its limits. Context Engineering, building Memory systems, and combining Multi-Agent architecture (multiple agents collaborating and challenging each other) are the keys to bringing AI into complex business domains that require high accuracy, such as finance (VPBank) and project management (Amazon Q).
> 2. **Practical engineering always comes with understanding the limits of technology**:
>    * Engineers need to accept that LLMs are non-deterministic from the GPU hardware level and API batching mechanism. Instead of fully trusting `temp=0`, engineers need to design systems that tolerate variation and include verification mechanisms such as majority voting and guardrails.
> 3. **Solid cloud infrastructure is the foundation for optimization**:
>    * Whether building AI or traditional applications, infrastructure fundamentals such as CDN (CloudFront), WAF, isolated VPC, and least-privilege IAM always determine whether a product can move from PoC/Hackathon environments to Enterprise-Grade scale.

## Evidence photo

![Evidence photo from AWS Community Day Vietnam](images/aws-community-day-evidence.jpg)

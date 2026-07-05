# Accenture Custom Software Engineer (Associate) Prep Guide

This guide is designed to help you, **K. Reena**, prepare thoroughly for your upcoming interview for the **Custom Software Engineer** (Associate) role at Accenture (Hyderabad). It breaks down every section of your resume, provides detailed explanation templates, identifies potential technical questions, and maps them to the expectations of this specific role.

---

## 1. Role Context: What Accenture Expects

The **Custom Software Engineer Associate (0-2 years)** role at Accenture Technology Centers in India (ATCI) focuses on building, testing, and maintaining scalable software. Key focus areas include:
- **Strong Python Fundamentals**: Writing clean, maintainable, and object-oriented code.
- **Problem Solving**: Basic Data Structures & Algorithms (DS&A) and competitive programming awareness.
- **Backend & APIs**: Understanding of RESTful API development, data validation, and database operations.
- **Modern Software Engineering Practices**: Version control (Git), Agile/SDLC, unit testing, and cloud fundamentals.
- **Structured Communication**: Ability to clearly articulate project architectures and technical choices.

---

## 2. Deep-Dive: Data Analytics Intern (VOIS for Tech Program)

This internship shows your ability to work with real-world data and extract business value, proving your practical coding skills.

### How to Pitch This Experience (The 60-Second Summary)
> "During my internship at VOIS for Tech, I was responsible for the end-to-end data analytics pipeline for two real-world datasets. I cleaned and preprocessed the raw data using Python and Pandas, handling missing values and label inconsistencies. I then performed exploratory data analysis (EDA) to build interactive and static visualizations using Matplotlib, Seaborn, and Plotly. Finally, I conducted correlation and regression analysis to translate data patterns into five actionable business recommendations for content strategy and market positioning."

### Likely Interview Questions & Sample Answers

#### Q1: "How did you handle missing values and duplicates in Pandas?"
*   **Concepts to Know**: `dropna()`, `fillna()`, `duplicated()`, `drop_duplicates()`.
*   **Best Response**:
    > "First, I identified missing values using `df.isnull().sum()`. For numerical columns with low variance, I imputed missing values with the median (to avoid outlier distortion) using `df['column'].fillna(df['column'].median())`. For categorical fields, I either used the mode or categorized them as 'Unknown'. For duplicates, I used `df.duplicated()` to check the volume, and if they were true redundant rows, I removed them using `df.drop_duplicates(inplace=True)`."

#### Q2: "What is feature extraction, and how did you apply it in this project?"
*   **Concepts to Know**: Deriving new metrics from raw columns (e.g., extracting month/day from a timestamp, categorizing continuous variables into bins).
*   **Best Response**:
    > "Feature extraction involves transforming raw data into new variables that highlight patterns more clearly for analysis. In my project, I worked with temporal data. I extracted features like 'Day of the Week' and 'Hour of the Day' from raw timestamp columns using Pandas datetime attributes. This helped us identify peak activity hours and weekday vs. weekend user behavior."

#### Q3: "What is the difference between correlation and regression?"
*   **Concepts to Know**: Correlation measures strength and direction of a linear relationship ($r$ ranging from -1 to 1). Regression models the mathematical relationship to predict a dependent variable based on independent variables ($Y = mX + C$).
*   **Best Response**:
    > "Correlation measures the strength and direction of the linear relationship between two variables, but it does not imply causation. Regression goes a step further; it builds a mathematical model (like linear regression) to predict the value of a dependent variable based on one or more independent variables."

---

## 3. Project 1: LeetCode Problem Recommender

This project highlights backend design, caching strategies, API development, and frontend dashboard integration.

### Project Architecture

```mermaid
graph TD
    A[Streamlit Frontend Dashboard] -->|REST API Requests| B[FastAPI Backend Engine]
    B -->|Check Cache First| C[(Redis/In-Memory Two-Tier Cache)]
    C -->|Cache Miss| D[LeetCode GraphQL API]
    B -->|Data Validation| E[Pydantic Models]
    B -->|Weakness Scoring| F[Tag-Based Score Calculator]
    B -->|Unit Testing| G[pytest Suite]
```

### Key Technical Deep-Dives

#### A. Two-Tier Caching System
*   **Why use it?**: Reduces latency and avoids hitting external LeetCode API rate limits.
*   **How to explain it**:
    > "I architected a two-tier caching mechanism. The first tier is a fast **in-memory L1 cache** (local dictionary/memory) for instant access. The second tier **(L2 cache)** can persist data or act as a larger cache store. When a recommendation is requested, the system checks L1 cache first. If it's a miss, it checks the database/L2 cache. If it misses both, it queries the LeetCode GraphQL API, populates the caches, and returns the result. This keeps recommendation response latency extremely low."

#### B. GraphQL vs. REST APIs
*   **Why GraphQL?**: LeetCode's public data is exposed via a GraphQL endpoint. GraphQL allows requesting *only* the specific fields needed (preventing over-fetching).
*   **How to explain it**:
    > "GraphQL allows the client to request exactly the data fields they need in a single query. Unlike REST, where you might have to call multiple endpoints (e.g., `/user/profile` and `/user/submissions`) and fetch unnecessary data, GraphQL lets us query a single endpoint with a custom query payload, saving bandwidth and network overhead."

#### C. Tag-Based Weakness Scoring Engine
*   **How does it work?**:
    > "The system analyzes a user's solved LeetCode history. It tallies the number of attempted, solved, and failed problems grouped by tags (e.g., Dynamic Programming, Arrays, Stack). It computes a score where tags with high failure rates or low attempt counts get a higher 'weakness score'. The recommendation engine then prioritizes fetching problems belonging to these high-weakness tags."

#### D. Pydantic and pytest
*   **Pydantic**: Performs run-time data validation and parsing. It ensures that the JSON payloads received by your FastAPI endpoints conform to exact data types.
*   **pytest**: The testing framework. Be prepared to explain how you wrote tests:
    > "I used `pytest` along with FastAPI's `TestClient` to mock API requests. I wrote test cases to verify the recommendation logic, cache hits/misses, and response schemas, ensuring that code changes wouldn't break the application."

---

## 4. Project 2: Company based RAG Chatbot

This project demonstrates your skills in GenAI, Web Scraping, Vector Databases, and FastAPI.

### RAG Pipeline Architecture

```mermaid
graph LR
    A[Playwright Web Scraper] -->|Extract Text| B[Raw Text Documents]
    B -->|Text Splitter| C[Semantic Chunks]
    C -->|Embedding Model| D[ChromaDB Vector Store]
    E[User Query] -->|Embedding Model| F[Vector Query]
    F -->|Similarity Search| D
    D -->|Top-K Context Chunks| G[Prompt Builder]
    G -->|Context + Query| H[Groq LLM API]
    H -->|Accurate Answer| I[User]
```

### Key Technical Deep-Dives

#### A. Retrieval-Augmented Generation (RAG) vs. Fine-Tuning
*   **Why RAG?**: Dynamic, keeps data private, doesn't hallucinate as much, much cheaper than training/fine-tuning.
*   **How to explain it**:
    > "RAG is a technique where we retrieve relevant document snippets from a private dataset and inject them as context into the prompt of a Large Language Model (LLM). This allows the LLM to answer domain-specific questions accurately without the expensive process of fine-tuning the model weights. It also dramatically reduces AI hallucinations because the model is anchored to the provided context."

#### B. Vector Database (ChromaDB) & Embeddings
*   **How it works**:
    > "ChromaDB is an open-source vector database. I used Playwright to scrape company pages, split the raw text into smaller, overlapping semantic chunks (to preserve context), and passed them to an embedding model (like HuggingFace's `all-MiniLM-L6-v2`). The model converts text chunks into high-dimensional vector embeddings (numerical lists representing semantic meaning). These vectors are indexed in ChromaDB. When a user asks a query, the query is also converted to a vector, and ChromaDB performs a cosine similarity search to retrieve the most semantically related chunks."

#### C. Web Scraping with Playwright
*   **Why Playwright over BeautifulSoup?**: Playwright can scrape modern, dynamically rendered single-page applications (SPAs) because it runs a headless browser that executes JavaScript.
*   **How to explain it**:
    > "Traditional scrapers like BeautifulSoup struggle with JavaScript-heavy websites. I used Playwright because it launches a headless browser, executes the site's scripts, waits for dynamic elements to load, and then extracts the clean DOM content. I used it to scrape 5+ target web pages, which formed the knowledge base for the RAG chatbot."

---

## 5. Technical Skills Core Prep Cheat Sheet

You must be ready to answer foundational questions about the skills listed in your technical section.

### A. Python (Programming Language)

#### 1. Object-Oriented Programming (OOP)
*   **Inheritance**: A class inheriting attributes and methods from a parent class.
*   **Polymorphism**: The ability of different classes to respond to the same method call in their own way (e.g., method overriding).
*   **Encapsulation**: Restricting direct access to some of an object's components (using private variables, e.g., `_variable` or `__variable`).
*   **Abstraction**: Hiding complex implementation details and showing only the essential features (using abstract base classes via Python's `abc` module).

#### 2. Python Lists, Decorators, and Generators
*   **List Comprehensions**: A concise way to create lists.
    ```python
    squares = [x**2 for x in range(10) if x % 2 == 0]
    ```
*   **Decorators**: A function that takes another function as an argument, extends its behavior without modifying it explicitly, and returns it. (Commonly used for logging, auth, caching).
    ```python
    def my_decorator(func):
        def wrapper(*args, **kwargs):
            print("Before execution")
            result = func(*args, **kwargs)
            print("After execution")
            return result
        return wrapper
    ```
*   **Generators**: Functions that return an iterator using the `yield` keyword. Instead of storing the entire list in memory, they yield values one at a time, making them highly memory-efficient.

#### 3. Memory Management in Python
*   Python uses **reference counting** as its primary garbage collection mechanism. When an object's reference count drops to 0, it is immediately deallocated.
*   To handle circular references (e.g., Object A references Object B, and Object B references Object A, preventing reference count from ever reaching 0), Python uses a cyclic **Garbage Collector (gc module)** that runs periodically in the background.

---

### B. Databases & SQL

#### 1. PostgreSQL vs. ChromaDB (Relational vs. Vector)
*   **PostgreSQL**: A relational database (RDBMS) that stores structured data in tables with schemas, supports ACID transactions, and uses SQL for queries. Ideal for transactional applications, user accounts, and relational records.
*   **ChromaDB**: A vector database designed to store and query high-dimensional vector embeddings quickly using nearest-neighbor search algorithms (like HNSW). Ideal for semantic search, recommendation engines, and LLM context retrieval.

#### 2. SQL Joins
*   **INNER JOIN**: Returns records that have matching values in both tables.
*   **LEFT JOIN (or LEFT OUTER JOIN)**: Returns all records from the left table, and the matched records from the right table. If no match is found, NULL is returned for the right table.
*   **RIGHT JOIN**: Returns all records from the right table, and the matched records from the left.
*   **FULL JOIN**: Returns all records when there is a match in either left or right table.

#### 3. Database Indexes
*   An index is a data structure (typically a B-Tree in PostgreSQL) that improves the speed of data retrieval operations on a table at the cost of additional write time and storage space.
*   **Trade-off**: Querying is much faster, but `INSERT`, `UPDATE`, and `DELETE` operations become slightly slower because the index must also be updated.

---

### C. Backend & API Development (FastAPI / REST)

#### 1. What makes FastAPI special?
*   It is built on top of **Starlette** (for web capabilities) and **Pydantic** (for data validation).
*   It supports **asynchronous programming** out-of-the-box (`async def`), enabling high concurrency.
*   It automatically generates interactive OpenAPI/Swagger documentation (`/docs`).

#### 2. HTTP Request Methods
*   `GET`: Retrieve data (should have no side effects on server state).
*   `POST`: Create new resources.
*   `PUT`: Update/replace an existing resource entirely.
*   `PATCH`: Apply partial modifications to a resource.
*   `DELETE`: Remove a resource.

#### 3. Authentication & Security (JWT, bcrypt)
*   **bcrypt**: A password hashing function. You never store passwords in plain text. You hash them with a salt using bcrypt before storing them in PostgreSQL.
*   **JWT (JSON Web Token)**: An open standard used to securely transmit information between parties as a JSON object. It is signed (usually with a secret key) and contains claims (like user ID). Once logged in, the client sends this token in the `Authorization: Bearer <token>` header of subsequent requests, allowing stateless authentication.

---

## 6. Explaining the "Extras" on Your Resume

Interviewers love to ask about non-technical activities, hackathons, and certifications. They show leadership, drive, and soft skills.

### A. Hack for Impact Hackathon (2nd Place Winner, 2024)
*   **How to pitch it**:
    > "Our team built a Startup-Investor Matchmaking Platform to solve the problem of early-stage startups struggling to find matching venture capitalists. We competed against 50+ teams. I worked on the backend components, setting up the match filtering logic and database. We secured 2nd place, and the award was presented by Aman Gupta (CEO of BoAt), which was a huge validation of our teamwork, rapid prototyping, and presentation skills under a 24-hour time constraint."
*   **Why it helps**: Demonstrates teamwork, adaptability, capability to deliver under pressure, and business orientation.

### B. Certifications
*   **Oracle Cloud Infrastructure 2025 AI Foundations Associate & AWS Cloud Essentials**: Shows you understand cloud architecture, VMs (EC2), security, and storage services.
*   **Postman API Fundamentals**: Shows you know how to build, test, and document APIs professionally.
*   **GitHub Foundations**: Validates your fluency in version control, branches, pull requests, and collaborative workflows.
*   **Generative AI Basics**: Proves you are keeping up with industry shifts.

### C. Rungta Business Incubator (Member)
*   **How to pitch it**:
    > "As a member of the Rungta Business Incubator, I collaborated with early-stage student founders. I assisted in evaluating business models, analyzing market readiness, and providing constructive feedback on their product pitch presentations. This experience expanded my understanding of the startup ecosystem and taught me how technical systems must align with business goals."
*   **Why it helps**: Shows you aren't just a coder; you understand the business context behind the software you write—a crucial trait for a *Custom Software Engineer* who works on tailoring business solutions.

---

## 7. Mock Interview Prep: Standard Q&As

### Q1: "Describe a challenge you faced in one of your projects and how you solved it."
*   **Context**: Use the **STAR** method (Situation, Task, Action, Result) with your **LeetCode Problem Recommender** project.
*   **Response**:
    *   **Situation**: "While building the LeetCode Problem Recommender, our system suffered from slow response times because it had to query the LeetCode GraphQL API on every search."
    *   **Task**: "I needed to reduce recommendation latency to under 100 milliseconds and avoid triggering LeetCode's rate limits."
    *   **Action**: "I designed and implemented a two-tier caching mechanism. I used a fast L1 in-memory cache to store popular query results. If the data wasn't in memory, it checked our secondary cache layer. I also wrote helper routines to periodically update this cache asynchronously."
    *   **Result**: "This reduced average API latency by over 70%, allowing users to receive personalized recommendations almost instantly while eliminating redundant external network requests."

### Q2: "What is your understanding of the Software Development Life Cycle (SDLC) and Agile?"
*   **Response**:
    > "SDLC is the systematic process for planning, creating, testing, deploying, and maintaining software. In an **Agile** framework, instead of building the whole software at once (like Waterfall), we work in short, iterative cycles called **sprints** (typically 2 weeks). At the start of a sprint, we plan user stories. During the sprint, we hold daily standups to discuss progress and blockers. At the end, we do a sprint review/demo and a retrospective to continuously improve our development process. This allows us to adapt to changing business requirements quickly."

### Q3: "What are Git merge conflicts and how do you resolve them?"
*   **Response**:
    > "A merge conflict occurs when two developers modify the same line of a file on different branches, or when one developer deletes a file that another developer is modifying, and Git cannot automatically determine which version to keep. To resolve it, I open the affected files, identify the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`), discuss the changes with the other developer to understand which code is correct, manually edit the file to retain the desired code, remove the markers, stage the file with `git add`, and commit the resolution."

---

## 8. Comprehensive Mock Interview Questions Repository

To help you build rock-solid confidence, here is a categorized bank of additional questions often asked by Accenture interviewers for Python and Custom Software Engineering roles.

### Category A: Python Core & Advanced

#### Q1: What is the difference between list and tuple? When would you use a tuple?
*   **Answer**: 
    > "Lists are mutable, meaning we can modify their elements (add, remove, or change values) after creation. They are defined using square brackets `[]`. Tuples are immutable, meaning they cannot be modified after creation, and are defined using parentheses `()`. 
    > 
    > I would use a tuple for collections of data that must remain constant throughout the execution of the program (like coordinate values `(x, y)` or configurations). Because tuples are immutable, they are faster to iterate over than lists and can be used as keys in dictionaries, whereas lists cannot."

#### Q2: What is the difference between `is` and `==` in Python?
*   **Answer**: 
    > "`==` is the equality operator; it checks whether the values of two objects are equal. 
    > 
    > `is` is the identity operator; it checks whether two variables point to the exact same object in memory (i.e., they have the same memory address, which can be checked using `id()`). 
    > For example, if `a = [1, 2]` and `b = [1, 2]`, `a == b` is `True` because their contents are identical, but `a is b` is `False` because they are stored in different memory addresses."

#### Q3: What are `*args` and `**kwargs` in Python functions?
*   **Answer**: 
    > "`*args` and `**kwargs` allow a function to accept a variable number of arguments. 
    > - `*args` passes a variable-length, non-keyworded argument list as a **tuple** inside the function.
    > - `**kwargs` passes keyworded arguments as a **dictionary** inside the function.
    > This makes functions highly flexible when we don't know beforehand how many arguments a user might pass."

#### Q4: Explain the concept of decorators and how you might use them in a real-world API.
*   **Answer**:
    > "A decorator is a design pattern in Python that allows us to modify or extend the behavior of a function or class without permanently modifying its source code. It wraps the target function.
    > 
    > In a real-world API (like FastAPI), decorators are commonly used for:
    > 1. **Authentication**: Checking if a user's JWT token is valid before hitting a protected route.
    > 2. **Logging**: Recording how long a database query or API endpoint takes to execute.
    > 3. **Rate Limiting**: Restricting a user to a maximum of 100 requests per minute by intercepting requests."

#### Q5: What is the Global Interpreter Lock (GIL) in Python?
*   **Answer**:
    > "The GIL is a mutex (lock) that protects access to Python objects, preventing multiple native threads from executing Python bytecodes at once. This means that even on a multi-core CPU, standard Python threads run one after another rather than in parallel for CPU-bound tasks.
    > 
    > To achieve true parallelism in Python for CPU-bound tasks, we use the `multiprocessing` module (which spawns separate processes with their own memory space and Python interpreter) instead of standard `threading`."

---

### Category B: Databases & SQL

#### Q1: What is the difference between `GROUP BY` and `ORDER BY`?
*   **Answer**:
    > "`GROUP BY` groups rows that have the same values into summary rows (e.g., finding the average score for each topic). It is always used in combination with aggregate functions like `COUNT()`, `MAX()`, `MIN()`, `SUM()`, or `AVG()`.
    > 
    > `ORDER BY` simply sorts the resulting records in ascending (`ASC`) or descending (`DESC`) order based on one or more columns, without collapsing or summarizing rows."

#### Q2: What is the difference between `WHERE` and `HAVING` clauses?
*   **Answer**:
    > "The `WHERE` clause is used to filter records *before* any groupings are made. It cannot be used with aggregate functions.
    > 
    > The `HAVING` clause is used to filter groups created by the `GROUP BY` clause. It is executed *after* the groupings are created, meaning we can use aggregate functions with it. For example:
    > `SELECT tag, COUNT(*) FROM problems GROUP BY tag HAVING COUNT(*) > 5;`"

#### Q3: What are database transactions and what does ACID stand for?
*   **Answer**:
    > "A transaction is a single logical unit of database work (like transferring money from bank Account A to B, which requires updating both accounts). ACID defines the properties that guarantee database transactions are processed reliably:
    > - **Atomicity**: The entire transaction succeeds or fails as a single unit ('all or nothing').
    > - **Consistency**: A transaction takes the database from one valid state to another, preserving constraints.
    > - **Isolation**: Transactions running concurrently do not interfere with each other.
    > - **Durability**: Once a transaction is committed, its changes are permanently recorded in the database, even in the event of a system crash."

---

### Category C: APIs & Backend Development

#### Q1: What is the difference between Path Parameters and Query Parameters in REST APIs?
*   **Answer**:
    > "- **Path Parameters** are part of the URL path itself and are used to identify a *specific resource*. For example, in `/problems/{id}` (e.g., `/problems/101`), `101` is a path parameter identifying a specific problem.
    > - **Query Parameters** are key-value pairs appended to the end of the URL after a question mark `?` and are used to *filter, sort, or paginate* resources. For example, in `/problems?difficulty=easy&limit=10`, `difficulty` and `limit` are query parameters."

#### Q2: What is CORS (Cross-Origin Resource Sharing) and how do you handle it in FastAPI?
*   **Answer**:
    > "CORS is a browser security mechanism that restricts web pages from making requests to a different domain than the one that served the web page. If my Streamlit frontend runs on `localhost:8501` and my FastAPI backend runs on `localhost:8000`, the browser will block requests by default due to CORS.
    > 
    > In FastAPI, I handle this by importing and adding the `CORSMiddleware` to the application, specifying the allowed origins (e.g., `['http://localhost:8501']`), allowed HTTP methods, and headers."

#### Q3: How do you handle exceptions and return clean error messages in FastAPI?
*   **Answer**:
    > "I use FastAPI's built-in `HTTPException` class. When a validation fails or a resource is missing, I raise an exception with a specific HTTP status code and a descriptive detail. For example:
    > `raise HTTPException(status_code=404, detail="Problem not found")`
    > FastAPI automatically converts this exception into a clean, structured JSON response for the client."

---

### Category D: Generative AI, RAG & Web Scraping

#### Q1: In your RAG Chatbot, how did you choose the chunk size for text splitting? What happens if the chunk size is too small or too large?
*   **Answer**:
    > "Choosing the chunk size involves balancing semantic context and specificity. I split scraped text into chunks of about 500-1000 characters with an overlap of 100-200 characters using a recursive splitter.
    > - If chunks are **too small** (e.g., 50 characters), they might split sentences in half, losing the context and meaning.
    > - If chunks are **too large** (e.g., 5000 characters), they introduce irrelevant noise into the prompt context, increasing LLM tokens cost and diluting the precise answer. The overlap ensures that context bordering the split points isn't lost."

#### Q2: What is Cosine Similarity and how is it used in Vector Search?
*   **Answer**:
    > "Cosine similarity is a metric used to measure how similar two vectors are by calculating the cosine of the angle between them in a high-dimensional space. The value ranges from -1 to 1 (where 1 means the vectors point in the exact same direction, meaning they are semantically identical).
    > 
    > In vector search, we convert the user's query into a vector and use cosine similarity to rank all document chunk vectors in ChromaDB. The chunks with the highest cosine similarity are retrieved as the most relevant context."

---

### Category E: Software Engineering, Git & Agile

#### Q1: What is the difference between `git merge` and `git rebase`?
*   **Answer**:
    > "`git merge` combines changes from one branch into another by creating a new 'merge commit' in the history. It preserves the exact chronological history of how branches branched off and joined back, but it can make the commit graph look cluttered.
    > 
    > `git rebase` takes the commits from your branch and replays them on top of the target branch. This rewrites the commit history to create a clean, linear sequence of commits without merge commits, but it should be avoided on public/shared branches since it rewrites history."

#### Q2: Explain the differences between Unit Testing and Integration Testing.
*   **Answer**:
    > "- **Unit Testing** focuses on testing individual, isolated components of the codebase (like a single function or scoring calculator method) to ensure they work correctly. External dependencies (like APIs or databases) are usually mocked. I used `pytest` to write unit tests for my scoring algorithm.
    > - **Integration Testing** tests how multiple components or systems work together (for example, verifying that a FastAPI route successfully communicates with PostgreSQL, processes data, and returns the correct response)."

#### Q3: What is CI/CD and how have you used it?
*   **Answer**:
    > "CI/CD stands for Continuous Integration and Continuous Delivery/Deployment.
    > - **Continuous Integration (CI)** is the practice of automatically building and testing code whenever a team member pushes changes to the repository. I used **GitHub Actions** to trigger my `pytest` test suite automatically on every pull request to ensure no breaking changes are merged.
    > - **Continuous Delivery/Deployment (CD)** automatically deploys the successfully tested code to a staging or production server (like Render or AWS) so that updates are delivered to users automatically."

---

### Category F: Behavioral Questions (STAR Method)

#### Q1: "Tell me about a time you had to learn a new technology quickly to solve a problem."
*   **Answer**:
    *   **Situation**: "During a hackathon, our team decided to build a startup matching platform. We quickly realized we needed to scrape startup and investor information dynamically from multiple sources, but I had only used static scrapers before."
    *   **Task**: "I needed to learn how to crawl dynamic, JavaScript-rendered web pages efficiently within a 12-hour window."
    *   **Action**: "I researched modern headless browser tools and decided to learn **Playwright**. I read the documentation, built a small prototype script to handle lazy-loaded elements, set up standard exceptions for timeouts, and successfully integrated it with our data indexing pipeline."
    *   **Result**: "Within 6 hours, I had a working crawler that successfully indexed 50+ prospective listings. This data powered our matching algorithm, helping us win 2nd place out of 50+ teams."

#### Q2: "How do you handle feedback or criticism on your code?"
*   **Answer**:
    > "I view code reviews and feedback as opportunities to learn and grow. When someone critiques my code, I don't take it personally. I analyze their suggestions objectively. If the feedback is about optimizing a function or adhering to OOP best practices, I immediately implement the changes. If I have a different perspective, I present my reasoning calmly, back it up with performance data or design documentation, and discuss it with the team to find the best solution."

---

## 9. Final Checklist: What to Review the Night Before

1.  **Code Syntax**: Be comfortable writing basic Python functions on a virtual whiteboard (e.g., reversing a linked list, checking for cycles, finding duplicates in an array, or parsing JSON).
2.  **API Design**: Practice explaining how you would design a REST API from scratch (defining URLs, request/response bodies, status codes).
3.  **Project Walkthroughs**: Speak out loud! Practice explaining your two projects (LeetCode Recommender and RAG Chatbot) in 2 minutes each. Use terms like *FastAPI, Pydantic, GraphQL, ChromaDB, embeddings, Playwright, caching, and rate limiting*.
4.  **SQL Queries**: Review standard SQL query writing (joins, group by, order by, and aggregations like `COUNT`, `SUM`, `AVG`).



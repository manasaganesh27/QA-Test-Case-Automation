# QA Test Case Suite Automation using RAG, LLMs & MCP

## 📌 Project Overview

This project explores the automation of QA test case suite generation using **Generative AI, Retrieval-Augmented Generation (RAG), Large Language Models (LLMs), and MCP-based orchestration**.

The goal was to reduce the manual effort involved in creating test cases when a new epic or feature is introduced. Instead of creating test cases entirely from scratch, the system uses information from existing project documentation and historical QA test suites to generate relevant and structured test cases.

The solution was developed as a **Proof of Concept (PoC)** to explore how GenAI can be integrated into an existing software development and QA workflow.

---

## 🎯 Problem Statement

When a new epic is created, QA engineers typically need to analyze information from multiple sources before creating test cases:

* Jira acceptance criteria
* Epic description
* Functional specifications from Confluence
* Business processes
* Use cases
* Existing QA test cases
* Previously implemented epics

This process can be time-consuming and repetitive.

The objective of this PoC was to explore:

> **Can existing QA knowledge and documentation be used to automatically generate a relevant test case suite for a new epic?**

---

## 📥 Input Data

The system uses information related to the new epic along with historical QA data.

### New Epic Information

* Jira Acceptance Criteria
* Epic Description
* Functional Requirements
* Business Process
* Use Cases

### Historical Information

* Existing QA test cases
* Previously implemented epics
* Similar functionality and testing scenarios

The historical data was structured into a JSON-based format containing fields such as:

```json
{
  "epic": "Hotel Search Enhancement",
  "acceptance_criteria": "...",
  "epic_description": "...",
  "process": "...",
  "use_cases": "...",
  "tests": "..."
}
```

---

## 🧰 Technologies Used

| Technology            | Purpose                                  |
| --------------------- | ---------------------------------------- |
| Python                | Core implementation                      |
| Azure OpenAI          | LLM-based test case generation           |
| Sentence Transformers | Text embeddings                          |
| FAISS                 | Vector similarity search                 |
| RAG                   | Retrieval of relevant historical context |
| MCP                   | AI/tool orchestration                    |
| LangChain             | LLM and RAG experimentation              |
| Gradio                | Prototype UI                             |
| JSON / CSV            | Data storage and preprocessing           |

---

## 🧹 Data Preparation

One of the important parts of the project was preparing the existing QA data before using it with an LLM.

The preprocessing involved:

1. Cleaning the raw QA data
2. Removing unnecessary information
3. Structuring historical QA information
4. Splitting larger content into smaller chunks
5. Creating searchable test-case chunks
6. Generating embeddings
7. Preparing the data for similarity-based retrieval

The resulting chunks could then be searched to find historical test cases relevant to a new epic.

---

## 🔎 Retrieval-Augmented Generation (RAG)

The project uses **RAG** to provide the LLM with relevant project-specific context.

Instead of directly asking the LLM to generate test cases, the system first searches historical QA data for similar or relevant test scenarios.

The retrieved information is then provided to the LLM along with the details of the new epic.

This allows the generated test suite to take into account:

* Existing testing patterns
* Project-specific terminology
* Similar functionality
* Previously identified scenarios
* Business rules
* Historical test cases

RAG was particularly useful because the LLM could work with **project-specific information rather than relying only on its general knowledge**.

---

## 🧠 Embeddings & Vector Search

To retrieve semantically relevant test cases, I experimented with text embeddings and vector similarity search.

Text is converted into numerical representations called **embeddings**. These vectors can then be compared to identify semantically similar content.

For example, two test cases might use different wording but describe similar functionality.

The project explored:

* Sentence Transformer models
* `all-MiniLM-L6-v2`
* FAISS for vector similarity search
* Semantic retrieval of historical test cases

This helped in understanding how vector-based retrieval can be used for enterprise QA data.

---

## 🤖 LLM-Based Test Case Generation

After retrieving relevant historical test cases, the retrieved context and new epic information are provided to the LLM.

The LLM is then used to generate a structured QA test suite.

The generated scenarios can include:

* Functional test cases
* Positive scenarios
* Negative scenarios
* Edge cases
* Boundary conditions
* Acceptance-criteria-based scenarios
* Business-rule validation

The intention was not to simply copy existing test cases, but to use them as references and generate scenarios relevant to the new functionality.

---

## 🔗 MCP & Orchestration

The project also explored **Model Context Protocol (MCP)** and how AI workflows can be organized into separate responsibilities.

Instead of relying on one LLM call to perform the entire task, different stages of the workflow can be coordinated, such as:

* Retrieving relevant information
* Preparing context
* Generating test cases
* Processing feedback

This provided an opportunity to explore how LLM applications can be designed as more structured, tool-driven workflows rather than simple input-to-output model calls.

---

# ⚠️ Challenges Faced
## 1. Retrieval Quality

The quality of retrieved context had a direct impact on the quality of the generated test cases.

Poor retrieval could result in irrelevant historical test cases being passed to the LLM, which could then lead to less relevant output.

This made retrieval quality an important consideration when designing the RAG pipeline.

---

## 2. Context Size

Providing too much historical information to the LLM was not always beneficial.

Irrelevant context could introduce noise, increase token usage, and result in redundant or less focused test cases.

Therefore, the retrieval process needed to focus on finding **relevant context rather than simply retrieving a large amount of information**.

---

# 📝 QA Feedback Loop

Since generated test cases require validation, the PoC also considers a human-in-the-loop feedback mechanism.

A QA engineer can review the generated test cases and provide feedback such as:

* Accepted
* Needs modification
* Incorrect
* Missing scenario
* Duplicate scenario
* Additional edge case required

The feedback can be stored in a structured format such as CSV or a spreadsheet.

This creates the foundation for improving the retrieval, prompts, and test-case generation process over time.

### Automated Evaluation

Develop automated methods to evaluate:

* Acceptance criteria coverage
* Test case relevance
* Test case duplication
* Edge-case coverage
* Overall test coverage

# 🏁 Conclusion

This PoC explored how **RAG, LLMs, embeddings, vector search, prompt engineering, and MCP orchestration** can be combined to automate part of the QA test case creation process.

The primary objective was to reduce repetitive manual work while still keeping QA engineers involved in reviewing and validating the generated test suites.

The project provided hands-on experience in building a GenAI application around real-world enterprise data, including data preprocessing, semantic retrieval, LLM generation, prompt refinement, dependency management, and human feedback integration.


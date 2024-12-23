# COMP40525 – Intro to RD & SQLProgramming

## Details
	23205535 - Chungman Lee
## Report
 Open "Project_Report_Chungmen_Lee.pdf"
## Project Overview

This project focuses on creating a **database structure** with sample datasets for **ChainForge**, a platform for managing and analyzing workflows that utilize Large Language Models (LLMs). The database is designed to store and monitor LLM usage in ChainForge while also providing functionality to save and view workflow-related data.

---

## Data Generation

The data for this project was generated using Python scripts to simulate realistic usage scenarios in ChainForge. Below is a summary of the generated dataset:

- **Users & Workflows**:
  - **50 users** were created, each assigned to a single workflow (1:1 relationship).
- **Nodes**:
  - Workflows contain **2 to 30 nodes**, randomly generated based on the workflow's nature, totaling **777 nodes**.
  - **Node_Links**: 632 links describe the communication between nodes, respecting type-based constraints (e.g., not all nodes can be source or target nodes).
- **LLM Models**:
  - **16 LLMs** available for use in ChainForge workflows were included.
- **LLM APIs**:
  - Each workflow has **0 to 3 API keys**, resulting in **77 API keys** across the dataset.
- **Node LLM Models**:
  - Generated for **prompt nodes** and **LLM evaluator nodes**, with **95 entries** in total.
- **Results**:
  - Each node has **1 to 5 results**, totaling **2311 results** stored in the database.

---

## Purpose

This database is designed to achieve the following goals:

1. **Track LLM Usage**: Monitor the utilization of various LLMs across ChainForge workflows.
2. **Store Workflow Data**: Save detailed information about users, workflows, nodes, and their interactions.

---

## Database Structure

The database consists of the following tables:

1. **Users**: Stores user details.
2. **LLM_Models**: Contains information about available LLMs in ChainForge.
3. **LLM_API**: Stores API keys associated with each user.
4. **Workflows**: Represents workflows used by the users.
5. **Nodes**: Contains nodes generated within workflows.
6. **Node_Type**: Defines the types of nodes available.
7. **Node_Links**: Tracks communication between nodes.
8. **Node_LLM_Models**: Maps nodes to the LLMs they utilize.
9. **Node_Results**: Stores the results generated by nodes.

## Views
### **Work_flow_Results**
This view provides a comprehensive overview of the results generated by nodes within workflows.

- **Columns**:  
  `workflow_id`, `workflow_name`, `node_id`, `result_data`, `created_at`
- **Purpose**:  
  Allows easy access to workflow-related node results.
- **Example Use Case**:  
  Fetch all results generated by nodes for a specific workflow.

### **LLM_usage**
Tracks the usage of each LLM in workflows and ranks them based on usage frequency.

- **Columns**:  
  `model_id`, `model_name`, `usage_count`, `LLM_node_rank`
- **Purpose**:  
  Identify the most utilized LLMs in ChainForge workflows.
- **Example Use Case**:  
  Analyze LLM popularity to inform resource allocation.

### **Weekly_LLM_Usage_Trend**
Analyzes weekly LLM usage trends, including comparisons with previous weeks.

- **Columns**:  
  `model_id`, `model_name`, `week_number`, `weekly_usage_count`, `usage_change`, `trend`, `score`
- **Purpose**:  
  Monitor and identify weekly usage patterns.
- **Example Use Case**:  
  Track changes in LLM performance over time.

### **LLM_Final_Scores**
Calculates a final score for each LLM based on its cumulative usage and weekly trends.

- **Columns**:  
  `model_id`, `model_name`, `usage_count`, `weekly_usage_count`, `weekly_score`, `final_score`
- **Purpose**:  
  Combine long-term and short-term metrics for comprehensive LLM ranking.
- **Example Use Case**:  
  Prioritize LLMs based on performance metrics.

---

## Procedures and Triggers
### **Trigger: CreateDefaultWorkflow**
- **Description**:  
  Automatically creates a default workflow for a newly registered user.
- **Purpose**:  
  Simplify initial workflow setup for new users.
- **Example Use Case**:  
  A default workflow is generated automatically upon user creation.

### **Procedure: RecordResult**
- **Description**:  
  Inserts a result into the `Node_Results` table for a specified node.
- **Parameters**:  
  `node_id`, `result_data`
- **Purpose**:  
  Streamline the process of recording node results.
- **Example Use Case**:  
  Add results generated during node execution to the database.

---

## Example queries are at the end of the SQL fILE
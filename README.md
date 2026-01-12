# Data Analysis Agent with LangGraph & Python REPL

An intelligent data analysis assistant designed to automate data processing, visualization, and reporting workflows. This project utilizes **LangGraph** to orchestrate a multi-agent workflow and **Python REPL** to verify and execute code, ensuring accurate and actionable insights.

## 🚀 Key Features

*   **Agentic Workflow**: orchestrated by **LangGraph**, consisting of distinct nodes for:
    *   **Data Loading**: Seamlessly reads and prepares CSV data.
    *   **Analysis**: Generates Python code to analyze data and create visualizations (Matplotlib/Seaborn).
    *   **Reporting**: Validates findings and generates a comprehensive summary.
*   **Secure Code Execution**: Leverages `PythonREPLTool` from `langchain_experimental` to execute generated code in a controlled environment.
*   **LLM Integration**: Powered by **Groq** (using `llama-3.3-70b-versatile`) for high-speed and efficient reasoning.
*   **State Management**: Uses a typed `MessagesState` to maintain context (messages, dataframes, file paths) across the workflow.

## 🏗️ Architecture

The agent operates on a graph-based architecture with the following flow:

```mermaid
graph LR
    START --> load_data
    load_data --> analyze_data
    analyze_data --> generate_report
    generate_report --> END
```

### Nodes
1.  **`load_data`**: Reads the input CSV file path and loads it into a Pandas DataFrame.
2.  **`analyze_data`**: Receives the user query and data, generates Python code to visualize/analyze it, and executes the code.
3.  **`generate_report`**: Reviews the analysis output and user query to generate a final validation report.

## 🛠️ Prerequisites

*   **Python 3.x**
*   **Google Colab** (Recommended for easy setup) or a local Jupyter environment.
*   **API Keys**:
    *   `GROQ_API_KEY`: Required for the LLM.

### Dependencies
Install the required packages:

```bash
pip install langchain langchain-groq langchain-community langgraph langchain-experimental pandas matplotlib seaborn
```

## 📖 Usage

1.  **Setup Environment**:
    Ensure your `GROQ_API_KEY` is set in your environment (e.g., using `google.colab.userdata` or environment variables).

2.  **Define Inputs**:
    Specify the path to your CSV file and your analysis query.

    ```python
    inputs = {
        "file_path": "/path/to/your/data.csv",
        "messages": "Generate a countplot for categories."
    }
    ```

3.  **Run the Graph**:
    Compile and stream the graph to see the agent in action.

    ```python
    from langgraph.graph import StateGraph

    # ... (graph definition from notebook) ...

    for output in my_graph.stream(inputs):
        for key, value in output.items():
            print(f"Node '{key}':")
            print(value)
    ```

## 📂 File Structure

*   `2_PythonREPL_Data_Analysis_Agent.ipynb`: The main Jupyter Notebook containing the full implementation of the agent and workflow.

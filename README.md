# AI-agent-based-Deep-Research

1. Setup and Imports -
   Import necessary libraries: os, langchain_together, langgraph, tavily, and langchain_core.messages.
   Set API keys for:
   - Tavily (for web searching).
   - Together AI (for using a large language model).

2. Tavily Search Client Initialization -
   Create a TavilyClient instance.
   Define search_tavily(query) function:
   Perform an online search using Tavily.
   Fetch a maximum of 5 advanced search results.
   Return the search results.

4. Large Language Model Initialization -
   Initialize ChatTogether LLM with:
   Model: Mixtral-8x7B-Instruct-v0.1.
   Temperature: 0.2 for more factual answers.
   Maximum tokens: 1024 to allow long outputs.

5. Agent 1: Researcher Node -
   Define researcher_node(state) function:
   Accepts input query from the system state.
   Calls search_tavily() to gather related documents.
   Formats titles, URLs, and snippets into a combined string.
   Returns the query and the formatted documents.

6. Agent 2: Answer Drafter Node -
   Define answer_drafter_node(state) function:
   Takes the original query and the collected documents.
   Sends these as a conversation to the Together AI model using SystemMessage and HumanMessage.
   Receives and returns the drafted answer along with the original query and documents.

7. Workflow Creation Using LangGraph -
   Create a StateGraph with dict as the base data type.
   Add two nodes:
   "research_agent" assigned to researcher_node.
   "answer_drafter" assigned to answer_drafter_node.
   Set the entry point of the workflow to "research_agent".
   Create workflow edges:
   From "research_agent" to "answer_drafter".
   From "answer_drafter" to END.
   Compile the workflow for execution.

8. Execution Function -
   Define run_deep_research_agentic_system(user_query):
   Takes a user query as input.
   Passes it through the compiled workflow.
   Returns the final drafted answer.

🎯 Summary
   The system creates a dual-agent architecture where:
   1.The first agent gathers detailed online information.
   2.The second agent drafts a well-organized, human-readable final answer.
   3.LangGraph organizes the workflow between the agents.
   4.Tavily API enables real-time research.
   5.Together AI API helps in high-quality answer drafting.

# repo_adk
Repozytorium do tworzenia agentów w ADK 

adk web --reload_agents

1) 
vertexai_search_agent = Agent(
    name="vertexai_search_agent",
    model=Gemini(model=os.getenv("MODEL"), retry_options=retry_options),
    instruction="Use your search tool to look up facts.",
    tools=[vertexai_search_tool]
)

    tools=[
        AgentTool(vertexai_search_agent, skip_summarization=False),
        get_date
    ]

2)
cp langchain_tool_agent/.env function_tool_agent/.env
cp langchain_tool_agent/.env vertexai_search_tool_agent/.env

    tools = [
        # Use the LangchainTool wrapper...
        LangchainTool(
            # to pass in a LangChain tool.
            # In this case, the WikipediaQueryRun tool,
            # which requires the WikipediaAPIWrapper as
            # part of the tool.
            tool=WikipediaQueryRun(
              api_wrapper=WikipediaAPIWrapper()
            )
        )
    ]


Google Search (google_search): Allows the agent to perform web searches using Google Search. You simply add google_search to the agent's tools.

Code Execution (built_in_code_execution): This tool allows the agent to execute code, to perform calculations, data manipulation, or interact with other systems programmatically. You can use the pre-built VertexCodeInterpreter or any code executor that implements the BaseCodeExecutor interface.

Retrieval (retrieval): A package of tools designed to fetch information from various sources.

Vertex AI Search Tool (VertexAiSearchTool): This tool integrates with Google Cloud's Vertex AI Search service to allow the agent to search through your AI Applications data stores.

With your Google Cloud console window selected, open Cloud Shell by pressing the G key and then the S key on your keyboard. Alternatively, you can click the Activate Cloud Shell button (Activate Cloud Shell) in the upper right of the Cloud console.

Best practices for writing functions to be used as tools include
Fewer Parameters are Better: Minimize the number of parameters to reduce complexity.
Use Simple Data Types: Favor primitive data types like str and int over custom classes when possible.
Use Meaningful Names: The function's name and parameter names significantly influence how the LLM interprets and utilizes the tool. Choose names that clearly reflect the function's purpose and the meaning of its inputs.
Break Down Complex Functions: Instead of a single update_profile(profile: Profile) function, create separate functions like update_name(name: str), update_age(age: int), etc.
Return status: Include a "status" key in your return dictionary to indicate the overall outcome (e.g., "success", "error", "pending") to provide the LLM a clear signal about the operation's state.


Linki przydatne:

https://docs.cloud.google.com/architecture/ai-ml
https://docs.cloud.google.com/vertex-ai/generative-ai/docs/deploy/consumption-options
https://github.com/google/adk-web/blob/main/README.md



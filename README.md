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

# LangGraph Simple Chatbot

A step-by-step implementation of a sophisticated chatbot built with LangGraph, demonstrating the power of stateful multi-agent applications.

## 🌟 Features

- **Basic Conversation**: Core chatbot functionality with LLM integration
- **Tool Integration**: Ability to use external tools like web search
- **Memory Management**: Maintains conversation context across interactions
- **Human-in-the-Loop**: Routes complex queries to human operators
- **Custom State Management**: Uses customizable state to control behavior
- **Time Travel**: Rewind and explore alternative conversation paths

## 📋 Overview

This project implements a support chatbot using LangGraph, a framework for building stateful multi-agent applications with language models. The implementation follows a progressive approach, starting with a basic chatbot and gradually adding more sophisticated capabilities.

The chatbot is built as a state machine using LangGraph's `StateGraph`, with nodes representing different processing steps, edges defining the flow between these steps, and state management for maintaining conversation context.

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- OpenAI API key (or Anthropic API key if using Claude models)

### Installation

```bash
# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install required packages
pip install -U langgraph langsmith langchain_openai
# For Anthropic models: pip install -U langgraph langsmith langchain_anthropic
```

### Environment Setup

Create a `.env` file in the project root and add your API keys:

```
OPENAI_API_KEY=your_openai_api_key_here
# Or for Anthropic:
# ANTHROPIC_API_KEY=your_anthropic_api_key_here
```

## 💻 Usage

Run the Jupyter notebook `simplebot.ipynb` to interact with the chatbot:

```bash
jupyter notebook simplebot.ipynb
```

The notebook contains step-by-step implementation of the chatbot, with detailed explanations of each component.

## 🏗️ Project Structure

The chatbot is implemented in a Jupyter notebook with the following structure:

1. **Setup**: Installation of required packages and API key configuration
2. **Part 1: Basic Chatbot**: Implementation of a simple conversational agent
3. **Part 2: Tool Integration**: Adding external tools to enhance capabilities
4. **Part 3: Memory Management**: Implementing conversation memory
5. **Part 4: Human-in-the-Loop**: Adding human intervention for complex queries
6. **Part 5: Custom State**: Implementing custom state management
7. **Part 6: Time Travel**: Adding the ability to rewind and explore alternatives

## 🧩 Key Components

### State Definition

```python
class State(TypedDict):
    # Messages have the type "list". The `add_messages` function
    # in the annotation defines how this state key should be updated
    messages: Annotated[list, add_messages]
```

### Graph Construction

```python
graph_builder = StateGraph(State)
graph_builder.add_node("chatbot", chatbot)
graph_builder.add_edge(START, "chatbot")
graph_builder.add_edge("chatbot", END)
graph = graph_builder.compile()
```

### Interaction Loop

```python
def stream_graph_updates(user_input: str):
    for event in graph.stream({"messages": [{"role": "user", "content": user_input}]}):
        for value in event.values():
            print("Assistant:", value["messages"][-1].content)
```

## 🔍 Advanced Features

### Tool Integration

The chatbot can use external tools like web search to gather information when needed, enhancing its ability to provide accurate and up-to-date responses.

### Memory Management

Conversation history is maintained across interactions, allowing the chatbot to provide contextually relevant responses based on the entire conversation thread.

### Human-in-the-Loop

Complex queries that the AI cannot handle confidently can be routed to human operators, ensuring high-quality responses for all user inquiries.

### Time Travel

The system supports rewinding to previous states and exploring alternative conversation paths, which is valuable for debugging and experimentation.

## 📚 Credits

This project is based on the [LangGraph Quickstart Tutorial](https://langchain-ai.github.io/langgraph/tutorials/introduction/) by LangChain. The tutorial provides a comprehensive introduction to building stateful multi-agent applications using LangGraph.

Key concepts and implementation details are drawn from this tutorial, which covers:
- Building basic chatbots with LangGraph
- Enhancing chatbots with tools
- Adding memory to chatbots
- Implementing human-in-the-loop workflows
- Customizing state management
- Using time travel capabilities

## 📄 License

[MIT License](LICENSE)

---

*Note: This README provides an overview of the capabilities demonstrated in the LangGraph tutorial. For a complete understanding, refer to the full tutorial at the link provided in the Credits section.* 
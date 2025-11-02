# LangGraph Email Agent

An intelligent email classification and auto-response system built with LangGraph and OpenAI's GPT-4. This agent automatically reads, classifies, and drafts professional responses to customer emails based on intent, urgency, and topic.

## Features

- **Intelligent Email Classification**: Automatically categorizes emails into intents (question, bug, billing, feature request)
- **Urgency Detection**: Identifies urgency levels (low, medium, high, critical)
- **Topic Extraction**: Identifies the main topic of each email
- **Automated Response Generation**: Drafts professional, context-aware responses
- **State Management**: Uses LangGraph's state management with checkpointing for workflow persistence
- **Visual Workflow**: Generates a visual representation of the agent workflow

## Architecture

The system uses a LangGraph state machine with the following workflow:

```
START → read_email → classify_intent → write_response → send_reply → END
```

### State Structure

The agent maintains the following state:

- `email_id`: Unique identifier for the email
- `email_content`: The actual email content
- `sender_email`: Email address of the sender
- `classification`: Contains intent, urgency, topic, and summary
- `draft_response`: The generated response

## Prerequisites

- Python 3.8+
- OpenAI API key

## Installation

1. Clone the repository:
```bash
git clone <your-repo-url>
cd <your-repo-name>
```

2. Install dependencies:
```bash
pip install langgraph langchain-openai python-dotenv ipython
```

3. Create a `dev.env` file in the project root:
```env
OPENAI_API_KEY=your_openai_api_key_here
```

## Usage

### Basic Usage

```python
from your_module import app

# Create initial state with email content
initial_state = {
    "email_content": "I have an issue logging to SAP Fiori"
}

# Run the agent
result = app.invoke(
    initial_state, 
    config={"configurable": {"thread_id": "1"}}
)

# View the result
print(result)
```

### Email Classification Categories

**Intents:**
- `question`: General inquiries
- `bug`: Technical issues or problems
- `billing`: Payment or billing-related concerns
- `feature`: Feature requests or suggestions

**Urgency Levels:**
- `low`: Non-critical, can wait
- `medium`: Should be addressed soon
- `high`: Needs prompt attention
- `critical`: Requires immediate action

## Project Structure

```
.
├── dev.env                 # Environment variables
├── main.py                 # Main application code
└── README.md              # This file
```

## How It Works

1. **Read Email**: Receives the email content (placeholder function)
2. **Classify Intent**: Uses GPT-4 with structured output to classify the email
3. **Write Response**: Generates a professional response based on classification
4. **Send Reply**: Outputs the generated response (currently prints to console)

## State Persistence

The agent uses `InMemorySaver` for checkpointing, allowing you to:
- Track conversation history
- Resume from previous states
- Maintain context across multiple interactions

## Visualization

The project includes functionality to visualize the agent's workflow as a graph using Mermaid diagrams.

## Dependencies

- `langgraph`: State machine and workflow orchestration
- `langchain-openai`: OpenAI model integration
- `python-dotenv`: Environment variable management
- `IPython`: Display utilities

## Configuration

The agent uses GPT-4.1 as the default model. You can modify the model in the code:

```python
llm = ChatOpenAI(model="gpt-4.1", api_key=os.getenv("OPENAI_API_KEY"))
```

## Future Enhancements

- Implement actual email reading functionality
- Add email sending capabilities (SMTP integration)
- Expand classification categories
- Add human-in-the-loop approval for responses
- Implement more sophisticated context retrieval
- Add support for attachments
- Create a web interface

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.


# GitHub Copilot SDK Playground

A collection of example applications demonstrating the [GitHub Copilot SDK for Go](https://github.com/github/copilot-sdk). Learn how to build AI-powered assistants with custom tools, streaming responses, and interactive conversations.

## 📋 Prerequisites

- Go 1.26.5 or higher
- GitHub Copilot subscription

## 🚀 Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/p2well/gh-copilot-sdk-playground-go.git
   cd gh-copilot-sdk-playground-go
   ```

2. Install dependencies:
   ```bash
   go mod download
   ```

## 📦 Examples

### Basic Example (`cmd/basic`)

A simple example demonstrating the core features of the Copilot SDK:
- Tool definition with typed parameters and return values
- Streaming responses
- Session management

**Run:**
```bash
go run cmd/basic/main.go
```

**What it does:**
Sends a single prompt asking about weather in multiple cities and demonstrates how Copilot automatically calls the custom `get_weather` tool to fulfill the request.

### Weather Assistant (`cmd/weather-assistant`)

An interactive conversational assistant that showcases:
- Multi-turn conversations
- Interactive CLI interface
- Event-driven response handling
- Custom tool integration

**Run:**
```bash
go run cmd/weather-assistant/main.go
```

**Try these prompts:**
- "What's the weather in Paris?"
- "Compare weather in NYC and LA"
- "Is it raining in Seattle?"

Type `exit` to quit the assistant.

## 🛠️ Project Structure

```
gh-copilot-sdk-playground-go/
├── cmd/
│   ├── basic/           # Simple one-shot example
│   │   └── main.go
│   └── weather-assistant/  # Interactive multi-turn example
│       └── main.go
├── go.mod
└── README.md
```

## 📚 Key Concepts

### Tool Definition

Tools allow Copilot to interact with external systems or perform specific actions:

```go
getWeather := copilot.DefineTool(
    "get_weather",
    "Get the current weather for a city",
    func(params WeatherParams, inv copilot.ToolInvocation) (WeatherResult, error) {
        // Implementation
    },
)
```

### Session Management

Sessions maintain conversation context and handle streaming responses:

```go
session, err := client.CreateSession(ctx, &copilot.SessionConfig{
    Model:     "gpt-4.1",
    Streaming: true,
    Tools:     []copilot.Tool{getWeather},
})
```

### Event Handling

Process streaming responses in real-time:

```go
session.On(func(event copilot.SessionEvent) {
    if event.Type == "assistant.message_delta" {
        fmt.Print(*event.Data.DeltaContent)
    }
})
```

## 🤝 Contributing

Contributions are welcome! Feel free to submit issues or pull requests.

## 📄 License

See [LICENSE](LICENSE) for details.

## 🔗 Resources

- [GitHub Copilot SDK Documentation](https://github.com/github/copilot-sdk)
- [GitHub Copilot](https://github.com/features/copilot)

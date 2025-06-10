# Echo Agent

## Overview

This document describes the implementation of an asynchronous echo agent using the `acp_sdk` library. The agent is designed to echo back input messages while simulating processing time and internal thoughts.

## Code Implementation

```python
@server.agent()
async def echo1(
    input: list[Message], context: Context
) -> AsyncGenerator[RunYield, RunYieldResume]:
    """Echoes everything"""
    for message in input:
        await asyncio.sleep(0.5)
        yield {"thought": "I should echo everything"}
        await asyncio.sleep(0.5)
        yield message
```

```python
server.run()
```

## Function Details

### Agent Registration
```python
@server.agent()
async def echo1(input: list[Message], context: Context)
```

The `echo1` function is decorated with `@server.agent()`, which registers it as an agent with the `Server` instance. This decorator makes the function accessible as a REST endpoint.

### Parameters
- **`input`**: A list of `Message` objects representing the incoming messages to process
- **`context`**: A `Context` object that provides contextual information about the agent's execution environment

### Return Type
The function returns an `AsyncGenerator[RunYield, RunYieldResume]`, allowing it to yield results asynchronously during execution.

## Functionality

The agent implements the following behavior:

1. **Message Processing**: Iterates through each `Message` object in the input list
2. **Simulated Processing**: Introduces 0.5-second delays using `asyncio.sleep(0.5)` to simulate processing time
3. **Thought Generation**: Yields intermediate thoughts as dictionaries:
   ```python
   yield {"thought": "I should echo everything"}
   ```
4. **Message Echoing**: Returns the original message back to the caller:
   ```python
   yield message
   ```

## Server Execution

The server is started with:
```python
server.run()
```

This call makes the `echo1` agent available for interaction through the server's REST API.

## Use Cases

This echo agent can be used for:
- Testing agent infrastructure
- Debugging message flow
- Demonstrating asynchronous agent patterns
- Simulating agent processing with delays

## Key Features

- **Asynchronous Processing**: Uses `async`/`await` patterns for non-blocking execution
- **Streaming Responses**: Yields results incrementally rather than waiting for completion
- **Simulated Intelligence**: Provides "thought" messages to simulate internal reasoning
- **Simple Echo Behavior**: Returns input messages unchanged for easy verification

# API Library Usage Example

This repository demonstrates how to use the `api` library to make HTTP requests in Go. The library supports JSON and XML responses and simplifies API integrations.

## Installation

To install the `api` library, run:

```bash
go get github.com/project-tech-3/api
```

## Example Usage

Below is an example program that demonstrates how to use the `api-go` library:

```go
package main

import (
	"fmt"
	"github.com/project-tech-3/api"
)

func main() {
	apiCfg := api.Api{}

	// Set the API endpoint URL
	apiCfg.Url = "https://api.github.com/users/tss182/repos"

	// Set the content type
	apiCfg.ContentType = api.TypeJson

	// Set the HTTP method
	apiCfg.Method = api.MethodGET

	// Execute the request
	err := apiCfg.Do()
	if err != nil {
		fmt.Println("Error:", err)
		return
	}

	// Parse the response into a Go struct
	var result []struct {
		ID       int    `json:"id"`
		NodeID   string `json:"node_id"`
		Name     string `json:"name"`
		FullName string `json:"full_name"`
		Private  bool   `json:"private"`
	}
	err = apiCfg.Get(&result)
	if err != nil {
		fmt.Println("Error parsing response:", err)
		return
	}

	// Print raw response
	fmt.Println("Raw Response:", apiCfg.GetRaw())

	// Print the parsed result
	fmt.Println("Parsed Result:", result)

	// Print HTTP status code
	fmt.Println("HTTP Status Code:", api.Status)
}
```

## Features

- **Supports JSON and XML responses**
- **Simplifies HTTP request handling**
- **Easily set headers, body, and method**

## Configuration

### Setting API URL
```go
apiCfg.Url = "https://api.example.com"
```

### Setting Content Type
```go
apiCfg.ContentType = api.TypeJson // or api.TypeXml
```

### Setting HTTP Method
```go
apiCfg.Method = api.MethodGET // or MethodPOST, MethodPUT, etc.
```

### Adding Headers
```go
apiCfg.HeaderAdd("Authorization", "Bearer <token>")
```

### Setting Request Body
For JSON payloads:
```go
apiCfg.Body = map[string]interface{}{
    "key": "value",
}
```

## Response Handling

### Parsing to a Struct
```go
var result YourStructType
err = apiCfg.Get(&result)
```

### Getting Raw Response
```go
fmt.Println(apiCfg.GetRaw())
```

### Getting HTTP Status
```go
fmt.Println(api.Status)
```

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

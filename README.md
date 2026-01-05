# gRPC Demo with Fern

This repository demonstrates how to use [Fern](https://buildwithfern.com) to generate API documentation from Protocol Buffer (`.proto`) files for gRPC services.

## Overview

Fern can parse your `.proto` files and generate beautiful, interactive API reference documentation. This demo includes a sample Plant Store API with two gRPC services:

- **PlantService**: Manage plant listings (create, read, update, delete, search)
- **OrderService**: Handle customer orders

## Repository Structure

```
fern/
├── fern.config.json      # Fern configuration with organization name
├── generators.yml        # API spec configuration pointing to proto files
├── docs.yml              # Documentation site configuration
└── proto/
    └── plantstore/
        └── v1/
            ├── plant_service.proto   # Plant management service
            └── order_service.proto   # Order management service
```

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) 18 or later
- [Fern CLI](https://docs.buildwithfern.com/learn/cli-api/cli-reference/commands)

### Install Fern CLI

```bash
npm install -g fern-api
```

### Generate Documentation

To preview your documentation locally:

```bash
fern docs dev
```

To generate and publish your documentation:

```bash
fern generate --docs
```

## Customizing for Your Own Project

To use this template for your own gRPC documentation:

### 1. Update the Organization Name

Edit `fern/fern.config.json` and replace the organization name:

```json
{
    "organization": "your-organization-name",
    "version": "3.32.0"
}
```

### 2. Update the Documentation URL

Edit `fern/docs.yml` and update the URL to your desired documentation domain:

```yaml
instances:
  - url: https://your-org.docs.buildwithfern.com
```

You can also customize the title, colors, and navigation in this file.

### 3. Replace the Proto Files

Replace the sample proto files in `fern/proto/` with your own:

1. Delete the existing `fern/proto/plantstore/` directory
2. Add your proto files following your package structure
3. Update `fern/generators.yml` to point to your proto files:

```yaml
api:
  specs:
    - proto:
        root: proto
        target: proto/your-package/v1/your_service.proto
        local-generation: true
```

### 4. Configure Proto Sources

The `generators.yml` file supports several options for proto files:

```yaml
api:
  specs:
    - proto:
        # Path to the proto directory root (where package paths start)
        root: proto
        
        # Optional: specific proto file to generate docs for
        # Omit to generate docs for all proto files in root
        target: proto/your-package/v1/service.proto
        
        # Whether to compile protos locally (default: false)
        local-generation: true
```

### 5. Customize Documentation Appearance

Edit `fern/docs.yml` to customize your documentation:

```yaml
instances:
  - url: https://your-org.docs.buildwithfern.com

title: Your API | Documentation

navigation:
  - api: API Reference
    paginated: true

colors:
  accentPrimary: '#your-brand-color'
  background: '#000000'

logo:
  dark: ./path/to/logo-dark.png
  light: ./path/to/logo-light.png
```

## Proto File Best Practices

For the best documentation output, follow these practices in your proto files:

### Add Comments for Documentation

Comments above services, RPCs, messages, and fields become documentation:

```protobuf
// UserService manages user accounts
service UserService {
  // Create a new user account
  rpc CreateUser(CreateUserRequest) returns (User);
}

message User {
  // Unique identifier for the user
  string id = 1;
}
```

### Use Descriptive Enum Values

```protobuf
enum Status {
  // Default unspecified status
  STATUS_UNSPECIFIED = 0;
  
  // User is active and can access the system
  STATUS_ACTIVE = 1;
}
```

### Organize with Packages

Use versioned packages for better organization:

```protobuf
syntax = "proto3";

package yourcompany.service.v1;
```

## Resources

- [Fern Documentation](https://docs.buildwithfern.com)
- [gRPC with Fern](https://docs.buildwithfern.com/api-definitions/grpc/overview)
- [Fern CLI Reference](https://docs.buildwithfern.com/learn/cli-api/cli-reference/commands)
- [Protocol Buffers Language Guide](https://protobuf.dev/programming-guides/proto3/)

## Support

For questions or issues with Fern, join the [Fern Community Slack](https://fern-community.slack.com/).

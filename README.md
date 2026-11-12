# Insurance Platform — System Analysis Project

System analysis project for an insurance platform covering policy calculation, policy issuance, integration flows, and policy refund.

## About the Project

The goal of the project was to design the main business and system flows for an insurance platform from the perspective of a System Analyst.

The project covers:

- insurance policy calculation;
- policy confirmation and registration;
- policy refund process;
- interaction between client applications and backend services;
- KYC and external system integrations;
- REST API design;
- business and system statuses;
- error handling;
- process and interaction diagrams.

## My Role

**System Analyst**

My responsibilities included:

- analyzing and formalizing business requirements;
- describing functional and non-functional requirements;
- preparing User Stories and Acceptance Criteria;
- designing business processes;
- creating BPMN and UML Sequence diagrams;
- designing REST API endpoints;
- defining request and response structures;
- describing system statuses and error scenarios;
- documenting integration flows;
- working with Swagger/OpenAPI.

## Main Business Flows

### 1. Policy Calculation

The user enters the required insurance information.

The system:

1. validates the input data;
2. sends the data to the backend;
3. calculates the insurance quote;
4. returns the calculated price and policy parameters to the client.

Example API flow:

```text
POST /v2/quote
```

The response contains the calculated insurance offer.

---

### 2. Policy Confirmation

After receiving the quote, the user confirms the insurance purchase.

Example:

```text
POST /v2/confirm
```

The backend:

1. validates the request;
2. performs required checks;
3. interacts with external services;
4. registers the insurance policy;
5. returns the result to the client.

Successful creation can return:

```text
HTTP 201 Created
```

The registered policy receives the status:

```text
REGISTERED
```

---

### 3. Policy Refund

The project also includes the refund process.

The user initiates a refund request for an existing insurance policy.

The system:

1. validates whether the policy can be refunded;
2. creates a refund request;
3. changes the status;
4. processes the refund;
5. updates the policy information.

Example intermediate status:

```text
REFUND_PENDING
```

The refund flow also considers payment and Wallet-related interactions.

## API Design

The API was designed using REST principles.

Main areas covered:

- quote calculation;
- policy confirmation;
- policy information;
- refund operations;
- validation and error responses.

Example endpoints:

```text
POST /v2/quote
POST /v2/confirm
```

Requests and responses are represented in JSON.

Example:

```json
{
  "productId": "INSURANCE_PRODUCT",
  "customerId": "12345",
  "parameters": {
    "coverage": "STANDARD"
  }
}
```

Example response:

```json
{
  "quoteId": "QT-10001",
  "status": "CALCULATED",
  "price": 15000
}
```

## Request Tracing

To simplify request tracking between services, the system uses a correlation identifier.

Example header:

```text
x-correlation-id
```

This allows the request to be traced across multiple components and integrations.

## Integrations

The solution considers interaction with external and internal systems, including:

- KYC services;
- government/external registry;
- payment services;
- Wallet;
- backend services.

Some external integrations can use SOAP through an ESB layer.

Simplified interaction:

```text
Client
   |
   v
Mobile / Web Application
   |
   v
API / Backend
   |
   +----> KYC
   |
   +----> Payment / Wallet
   |
   +----> ESB
             |
             v
        External Registry
```

## System Statuses

Example statuses used in the designed flows:

```text
REGISTERED
REFUND_PENDING
```

Statuses help control the lifecycle of an insurance policy and refund operation.

## Diagrams

The project includes system and business diagrams.

### BPMN

Used to describe business processes such as:

- insurance policy creation;
- validation;
- policy registration;
- refund processing.

### UML Sequence Diagram

Used to describe interactions between:

- User;
- Mobile/Web Application;
- Backend;
- KYC;
- Payment/Wallet;
- external services.

## Error Handling

The project considers both successful and alternative scenarios.

Examples:

- invalid input data;
- failed validation;
- KYC failure;
- external service unavailable;
- payment error;
- policy cannot be refunded;
- integration timeout.

For each scenario, the system should return an appropriate HTTP status and error response.

## Documentation

The project may include:

```text
Insurance-System-Analysis/
│
├── README.md
│
├── BPMN/
│   ├── policy_creation.png
│   └── policy_refund.png
│
├── Sequence/
│   ├── policy_confirmation.png
│   └── refund_sequence.png
│
├── API/
│   └── openapi.yaml
│
├── Use-Cases/
│   └── use-cases.pdf
│
└── Docs/
    └── system-analysis.pdf
```

## Tools

- Draw.io
- Swagger / OpenAPI
- SwaggerHub
- REST API
- JSON
- BPMN
- UML Sequence Diagram
- SQL
- Grafana

## Skills Demonstrated

This project demonstrates practical knowledge of:

- requirements analysis;
- business process modeling;
- REST API design;
- integration analysis;
- system statuses;
- error handling;
- BPMN;
- UML Sequence Diagram;
- OpenAPI / Swagger;
- client-server architecture;
- documentation of system behavior.

## Project Type

Educational System Analysis project.

The project was created to practice System Analyst responsibilities and demonstrate the ability to translate business scenarios into processes, API contracts, integrations, statuses, and technical documentation.

# TOON
TOON, or Token-Oriented Object Notation, is a compact, human-readable data serialization format designed specifically for interactions with Large Language Models (LLMs). 
It encodes JSON-compatible structures like objects, arrays, and primitives in a way that reduces token usage by 30-60% compared to standard JSON, making it more efficient for AI prompts and contexts while remaining easy for humans to parse. 
Unlike JSON's verbose punctuation-heavy syntax, TOON uses YAML-like indentation for nested objects and CSV-style tabular layouts for uniform arrays of objects, minimizing redundant elements like quotes and braces


Input JSON

invoice_data = {
        "company": "Acme Corp",
        "invoices": [
            {
                "id": "INV001",
                "customer": "Alice Ltd",
                "date": "2025-11-15",
                "items": ["Widget A", "Widget B"],
                "total": 1250.00,
                "due": "2025-12-15",
                "status": "pending"
            },
            {
                "id": "INV002", 
                "customer": "Bob Inc",
                "date": "2025-11-20",
                "items": ["Gadget X"],
                "total": 890.50,
                "due": "2025-12-20",
                "status": "paid"
            },
            {
                "id": "INV003",
                "customer": "Charlie Co",
                "date": "2025-11-25",
                "items": ["Service Y", "Service Z"],
                "total": 3400.00,
                "due": "2025-12-25",
                "status": "pending"
            }
        ]
    }
    {
    "company": "Acme Corp",
    "invoices": [
        {"id": "INV001", "customer": "Alice Ltd", "date": "2025-11-15", "items": ["Widget A", "Widget B"], "total": 1250.00, "due": "2025-12-15", "status": "pending"},
        {"id": "INV002", "customer": "Bob Inc", "date": "2025-11-20", "items": ["Gadget X"], "total": 890.50, "due": "2025-12-20", "status": "paid"},
        {"id": "INV003", "customer": "Charlie Co", "date": "2025-11-25", "items": ["Service Y", "Service Z"], "total": 3400.00, "due": "2025-12-25", "status": "pending"}
    ]
    }


TOON 

company: Acme Corp
invoices[3]:
- id: INV001
customer: Alice Ltd
date: 2025-11-15
items[2]: Widget A,Widget B
total: 1250.0
due: 2025-12-15
status: pending
- id: INV002
customer: Bob Inc
date: 2025-11-20
items[1]: Gadget X
total: 890.5
due: 2025-12-20
status: paid
- id: INV003
customer: Charlie Co
date: 2025-11-25
items[2]: Service Y,Service Z
total: 3400.0
due: 2025-12-25
status: pending


**Model Output**

The invoices for Charlie Co. are:
- id: INV003
customer: Charlie Co
date: 2025-11-25
items[2]: Service Y,Service Z
total: 3400.0
due: 2025-12-25
status: pending


Reponse by passing TOON datatype 

{
   "ResponseMetadata":{
      "RequestId":"f9bbf132-b5c3-4065-ad89-3ba00929deee",
      "HTTPStatusCode":200,
      "HTTPHeaders":{
         "date":"Sun, 30 Nov 2025 17:12:47 GMT",
         "content-type":"application/json",
         "content-length":"425",
         "connection":"keep-alive",
         "x-amzn-requestid":"f9bbf132-b5c3-4065-ad89-3ba00929deee",
         "x-amzn-bedrock-invocation-latency":"615",
         "x-amzn-bedrock-output-token-count":"72",
         "x-amzn-bedrock-input-token-count":"224"
      },
      "RetryAttempts":0
   },
   "contentType":"application/json",
   "body":<botocore.response.StreamingBody object at 0x7f9cc02f0370>
}


Reponse by passing JSON datatype

{
   "ResponseMetadata":{
      "RequestId":"9bb9ad60-c640-4f66-867e-cf7479068d17",
      "HTTPStatusCode":200,
      "HTTPHeaders":{
         "date":"Sun, 30 Nov 2025 17:12:48 GMT",
         "content-type":"application/json",
         "content-length":"608",
         "connection":"keep-alive",
         "x-amzn-requestid":"9bb9ad60-c640-4f66-867e-cf7479068d17",
         "x-amzn-bedrock-invocation-latency":"1021",
         "x-amzn-bedrock-output-token-count":"120",
         "x-amzn-bedrock-input-token-count":"264"
      },
      "RetryAttempts":0
   },
   "contentType":"application/json",
   "body":<botocore.response.StreamingBody object at 0x7f9cc02f0790>
}

Summary of Improvements

| Metric            | JSON    | TOON   | % Reduction |
| ----------------- | ------- | ------ | ----------- |
| Input Tokens      | 264     | 224    | 15.15%      |
| Output Tokens     | 120     | 72     | 40%         |
| Latency           | 1021 ms | 615 ms | 39.8%       |

Note: This is just an example, the metrics varies depending on the nature of input



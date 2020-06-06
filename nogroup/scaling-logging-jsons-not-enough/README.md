# Scaling Logging: JSON's Not Enough

JSON is the de-facto log standard. JSON's native support makes it an evolution over text based logs. JSON is so ubiquitous that the popular logging data tools (such as Elasticsearch) accept JSON by default. JSON's lack of strict types make it insufficient to use as a multi-service or long term log format. This post describes the problem with JSON and proposes a solution using a strictly typed interchange format such as Protocol Buffers.

# The Trouble With JSON

## An Evolution
## Scales Until
## Feedback loops

# Strict Types 

## Wire Protocols 

# Conclusion

--- 
# Outline
- Intro
    - JSON - defacto
    - Missing explicit types
    - Explicit schema using a technology like Protocol Buffers
- The trouble with JSON
    - Structure vs Unstructured
    - not untyped
        - No regex
    - Feedback loops
    - Schema on Read vs Write
- Strict Types
    - Protocol Buffers to the rescue 
    - Strict types
    - Cross language bindings
    - Wire protocols
    - Feedback loops
    - Schema on write
    - Aggregation
    - Downstream services 
- Conclusion

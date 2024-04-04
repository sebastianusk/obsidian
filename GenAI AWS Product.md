---
tags:
  - zettelkasten
topic: 
createAt: 2024-04-03 21:16
---
This simple setup can help us to play around GenAI with our central knowledge document. Step to set up:
- create S3
- fill S3 with the Documents
- create Bedrock Knowledge base, attach the S3
- create Bedrock Foundation (this is the normal LLM)
- create prompt engineering where the flow will use Bedrock Knowledge base to get the vector DB, then make conclusion using the Bedrock Foundation
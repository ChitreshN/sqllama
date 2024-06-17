# Sql llm server

* An llm hacked together to process natural language queries and produce sql queries
given the context, that is the create table statements correspondig to the db

# Installation

```bash
git clone
cd sqllama

```

## Build

```bash
make
```

# Running the server

* Before running the server get the gguf file from [here](https://huggingface.co/PrunaAI/defog-llama-3-sqlcoder-8b-GGUF-smashed/tree/main)
* The name of the file is llama-3-sqlcoder-8b.Q4_K_M.gguf
* And place it in the models directory
* Run the following command to start the server to listen for requests

```bash
./server -m ./models/llama-3-sqlcoder-8b.Q4_K_M.gguf -c 2048
```

* To make use of gpu in the system if available refer to [llama.cpp](https://github.com/ggerganov/llama.cpp/)

# Request format

* for completions follow the below example request
```bash
curl --url localhost:8080/completion \
                                            --request POST \
                                            --data '{
                                            "prompt": <|start_header_id|>user<|end_header_id|> Generate a SQL query to answer this question: `{user_question}` {instructions} DDL statements: {create_table_statements}<|eot_id|> <|start_header_id|>assistant<|end_header_id|> The following SQL query best answers the question `{user_question}` \n ``` sql:
                                        }'
```

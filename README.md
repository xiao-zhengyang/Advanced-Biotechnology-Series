# Advanced-Biotechnology-Series
## Network for Knowledge Organization (NEKO): a universal knowledge mining workflow
![image](https://github.com/user-attachments/assets/9fe8f676-cb6f-4b2e-a525-fbebbc648b2f)

## Use LLM for bioprocess data extraction**
![image](https://github.com/user-attachments/assets/d20f4552-baf0-4e3d-a55c-f7d379364821)



## GraphRAG  

**GraphRAG** is an advanced framework to enhance LLMs in generating domain-specific outputs. It integrates three query modes—global, local, and DRIFT search—for comprehensive question-answering through natural language input. Below are steps to use LLM and GraphRAG for studying β-carotene production in *Yarrowia lipolytica*.  

---

### Steps  

#### Step 1: Configure Ollama LLM  
Ollama’s default LLM contexts (e.g., 2k tokens) truncate long texts. Create a customized LLM with extended context:  

1. Generate a `settings.txt` file and modify it:  
   ``` 
   ollama create qwen2.5:14b_8k -f settings.txt  
   ```  
2. Add the following line to `settings.txt`:  
   ```  
   PARAMETER num_ctx 4096  
   ```  

#### Step 2: Initialize GraphRAG and Prompt Tuning  
1. Install GraphRAG (version 1.2.0):  
   ``` 
   pip install graphrag==1.2.0  
   ```  
2. Initialize a new project:  
   ``` 
   graphrag init --root ./[Yarrowia_local]  
   ```  
   A preconfigured project with input text is available in the [GitHub repository](https://github.com/xiao-zhengyang/Advanced-Biotechnology-Series/tree/main/GraphRAG).  

**Notes**:  
- For systems without GPU, set `request_timeout ≥ 10,000` in `settings.yaml`.  
- Use the `autotune` command to generate context-aware prompts:  
   ```
   python -m graphrag prompt-tune --root ./[Yarrowia_local] --config ./[Yarrowia_local]/settings_prompt_tune.yaml  
   ```  
- Use large-parameter LLMs (>70B) like **GPT-4o** or **Qwen2.5-instruct-72B** for prompt tuning. Replace the OpenAI API key in `settings_prompt_tune.yaml`.  

#### Step 3: Indexing the Input Text  
Execute indexing to generate a structured knowledge graph:  
```
graphrag index --root ./[Yarrowia_local]  
```  

**Processing Times**:  
- CPU: >10 hours  
- GPU: <30 minutes  

#### Step 4: Querying and Visualization  
GraphRAG supports three query modes:  
1. **Global Search**: High-level summaries of broad topics.  
2. **Local Search**: Retrieves detailed information.  
3. **DRIFT Search**: Context-aware dynamic querying.  

Visualize the knowledge graph (`output/` folder) using tools like **Gephi** or **Cytoscape** to explore connections.  

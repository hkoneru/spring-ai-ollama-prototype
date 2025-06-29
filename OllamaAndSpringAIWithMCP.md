  Interactive Guide: Spring Boot AI with Ollama & RAG & MCP      body { font-family: 'Inter', sans-serif; background-color: #f5f5f4; /\* stone-100 \*/ color: #374151; /\* gray-700 \*/ } .nav-link.active { color: #3b82f6; /\* blue-500 \*/ font-weight: 600; } .code-block { position: relative; background-color: #1f2937; /\* gray-800 \*/ color: #d1d5db; /\* gray-300 \*/ border-radius: 0.5rem; padding: 1rem; overflow-x: auto; font-family: 'Courier New', Courier, monospace; font-size: 0.875rem; } .copy-btn { position: absolute; top: 0.5rem; right: 0.5rem; background-color: #4b5563; /\* gray-600 \*/ color: white; border: none; padding: 0.25rem 0.5rem; border-radius: 0.25rem; cursor: pointer; font-size: 0.75rem; opacity: 0.5; transition: opacity 0.2s; } .code-block:hover .copy-btn { opacity: 1; } .syntax-keyword { color: #93c5fd; } /\* blue-300 \*/ .syntax-string { color: #a5b4fc; } /\* indigo-300 \*/ .syntax-comment { color: #9ca3af; } /\* gray-400 \*/ .syntax-class { color: #6ee7b7; } /\* emerald-300 \*/ .syntax-annotation { color: #fde047; } /\* yellow-300 \*/ .syntax-number { color: #f9a8d4; } /\* pink-300 \*/ .syntax-method { color: #818cf8; } /\* violet-400 \*/ .diagram-arrow { position: relative; width: 2.5rem; height: 2px; background-color: #9ca3af; } .diagram-arrow::after { content: ''; position: absolute; right: -2px; top: -4px; border: solid #9ca3af; border-width: 0 2px 2px 0; display: inline-block; padding: 4px; transform: rotate(-45deg); }

Ollama & Spring AI Guide
========================

[Overview](#overview) [How It Works](#how-it-works) [Setup](#setup) [Code](#code) [Run & Test](#run)

Open main menu

[Overview](#overview) [How It Works](#how-it-works) [Setup](#setup) [Code](#code) [Run & Test](#run)

Build a Local AI with Spring Boot, Ollama & RAG
-----------------------------------------------

This guide provides an interactive walkthrough for integrating a local Ollama language model into a Java Spring Boot project using a Retrieval Augmented Generation (RAG) pipeline to query your own documents, now enhanced with Spring AI's Model Context Protocol (MCP) for dynamic context retrieval.

### Local & Private AI

Use Ollama to run powerful language models entirely on your local machine, ensuring data privacy and offline capability.

### Simplified Integration

Spring AI provides a unified, abstract API to seamlessly connect your Java application with AI models and vector stores.

### Custom Knowledge (RAG)

Leverage the RAG pattern to "train" the model with your documents, enabling it to answer questions based on your specific data.

### Dynamic Context (MCP)

Utilize Spring AI MCP to define custom tools that the LLM can call, like reading file system content, to gather real-time context.

How It Works: The RAG & MCP Pipeline
------------------------------------

This diagram illustrates how a user's question is answered by integrating both RAG and dynamic tool calls through Spring AI's Model Context Protocol (MCP).

❓

#### 1\. User Query

User asks a question.

🧠

#### 2\. LLM Decides

LLM determines if a tool or RAG is needed.

🛠️

#### 3\. Tool Call (MCP)

LLM calls a custom Java tool for dynamic context (e.g., file content).

📚

#### 4\. Retrieve (RAG)

Search Vector Store for relevant document chunks.

➕

#### 5\. Augment

Combine query, tool output, and RAG docs into a prompt.

🤖

#### 6\. Generate

LLM generates answer based on all available context.

💡

#### 7\. Response

The final, contextual answer is returned.

Project Setup & Configuration
-----------------------------

Follow these steps to configure your Spring Boot project, now including Spring AI's Model Context Protocol (MCP) for dynamic tool interactions.

Prerequisites pom.xml application.properties

*   Java Development Kit (JDK) 17+
*   Maven 3.6+
*   Ollama Installed and Running
    
    Ensure you have pulled the required models:
    
    Copy `ollama pull gemma:2b   ollama pull nomic-embed-text`
    

Copy

Copy

Java Code Walkthrough
---------------------

Explore the key Java classes that power the RAG pipeline and the new custom tool for dynamic context retrieval using Spring AI MCP.

### Project Files

*   AIController.java
*   AIService.java
*   DocumentIngestionService.java
*   FileContentTool.java
*   VectorStoreConfig.java
*   qa-system-prompt.st

Copy

Run & Test Your Application
---------------------------

Once your code is in place, follow these steps to run the application, ingest your documents, and test both RAG and MCP functionalities.

### Step 1: Build and Run the Spring App

Open your terminal in the project root and execute the Maven command to start your application.

Copy `mvn spring-boot:run`

### Step 2: Ingest Your Documents (RAG)

Use \`curl\` or any API client to send a POST request to the \`/ingest-docs\` endpoint. This loads your documents into the vector store for RAG.

Copy `curl -X POST http://localhost:8080/api/ai/ingest-docs`

### Step 3: Ask Questions (RAG & MCP)

Now, ask questions. The model will decide whether to use the RAG pipeline or call your custom \`getFileContent\` tool based on the prompt.

Copy `curl "http://localhost:8080/api/ai/ask?question=What+is+the+Amazon+Rainforest?"`

Expected (RAG) Output: The Amazon Rainforest is the largest rainforest in the world...

Copy `curl "http://localhost:8080/api/ai/ask?question=Can+you+tell+me+about+the+content+of+file+important.txt?"`

Expected (MCP) Output: The content of important.txt is: "This is very important information for the project."

Interactive Guide generated from source material. All content is for educational purposes.

document.addEventListener('DOMContentLoaded', function() { const codeData = { pom: \` <span class="syntax-comment">&lt;!-- Use the latest stable Spring Boot version --&gt;</span> &lt;parent&gt; &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt; &lt;artifactId&gt;spring-boot-starter-parent&lt;/artifactId&gt; &lt;version&gt;3.2.7&lt;/version&gt; &lt;/parent&gt; <span class="syntax-comment">&lt;!-- ... --&gt;</span> &lt;properties&gt; &lt;java.version&gt;21&lt;/java.version&gt; &lt;spring-ai.version&gt;0.8.1&lt;/spring-ai.version&gt; &lt;/properties&gt; &lt;dependencies&gt; &lt;dependency&gt; &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt; &lt;artifactId&gt;spring-boot-starter-web&lt;/artifactId&gt; &lt;/dependency&gt; &lt;dependency&gt; &lt;groupId&gt;org.springframework.ai&lt;/groupId&gt; &lt;artifactId&gt;spring-ai-ollama-spring-boot-starter&lt;/artifactId&gt; &lt;/dependency&gt; &lt;dependency&gt; &lt;groupId&gt;org.springframework.ai&lt;/groupId&gt; &lt;artifactId&gt;spring-ai-core&lt;/artifactId&gt; &lt;/dependency&gt; <span class="syntax-comment">&lt;!-- New: Spring AI MCP Starter for Tool Calling --&gt;</span> &lt;dependency&gt; &lt;groupId&gt;org.springframework.ai&lt;/groupId&gt; &lt;artifactId&gt;spring-ai-mcp-spring-boot-starter&lt;/artifactId&gt; &lt;/dependency&gt; &lt;/dependencies&gt; &lt;dependencyManagement&gt; &lt;dependencies&gt; &lt;dependency&gt; &lt;groupId&gt;org.springframework.ai&lt;/groupId&gt; &lt;artifactId&gt;spring-ai-bom&lt;/artifactId&gt; &lt;version&gt;\\${spring-ai.version}&lt;/version&gt; &lt;type&gt;pom&lt;/type&gt; &lt;scope&gt;import&lt;/scope&gt; &lt;/dependency&gt; &lt;/dependencies&gt; &lt;/dependencyManagement&gt; \`, properties: \` <span class="syntax-comment"># Ollama server URL (default)</span> <span class="syntax-keyword">spring.ai.ollama.base-url</span>=<span class="syntax-string">http://localhost:11434</span> <span class="syntax-comment"># Specify the chat model to use (must be pulled in Ollama)</span> <span class="syntax-keyword">spring.ai.ollama.chat.options.model</span>=<span class="syntax-string">gemma:2b</span> <span class="syntax-comment"># Specify the embedding model to use (must be pulled in Ollama)</span> <span class="syntax-keyword">spring.ai.ollama.embedding.options.model</span>=<span class="syntax-string">nomic-embed-text</span> <span class="syntax-comment"># Optional: Automatically pull the model if not found locally</span> <span class="syntax-keyword">spring.ai.ollama.init.pull-model-strategy</span>=<span class="syntax-string">when\_missing</span> <span class="syntax-comment"># MCP configuration (usually default for basic tools)</span> <span class="syntax-comment"># spring.ai.mcp.enabled=true</span> \`, controller: { explanation: '<h4 class="font-semibold">AIController.java</h4><p class="text-sm text-gray-600 mt-1">This class exposes REST endpoints. It allows users to trigger document ingestion via a POST request for RAG and ask questions via a GET request, where the AI model might utilize both RAG and custom tools (MCP).</p>', code: \` <span class="syntax-keyword">package</span> com.example.ollamaragapp.controller; <span class="syntax-keyword">import</span> com.example.ollamaragapp.service.AIService; <span class="syntax-keyword">import</span> com.example.ollamaragapp.service.DocumentIngestionService; <span class="syntax-keyword">import</span> org.springframework.web.bind.annotation.\*; <span class="syntax-annotation">@RestController</span> <span class="syntax-annotation">@RequestMapping</span>(<span class="syntax-string">"/api/ai"</span>) <span class="syntax-keyword">public class</span> <span class="syntax-class">AIController</span> { <span class="syntax-keyword">private final</span> AIService aiService; <span class="syntax-keyword">private final</span> DocumentIngestionService documentIngestionService; <span class="syntax-keyword">public</span> <span class="syntax-class">AIController</span>(AIService aiService, DocumentIngestionService d) { <span class="syntax-keyword">this</span>.aiService = aiService; <span class="syntax-keyword">this</span>.documentIngestionService = d; } <span class="syntax-annotation">@PostMapping</span>(<span class="syntax-string">"/ingest-docs"</span>) <span class="syntax-keyword">public</span> String <span class="syntax-class">ingestDocuments</span>() { documentIngestionService.ingestDocuments(); <span class="syntax-keyword">return</span> <span class="syntax-string">"Document ingestion initiated."</span>; } <span class="syntax-annotation">@GetMapping</span>(<span class="syntax-string">"/ask"</span>) <span class="syntax-keyword">public</span> String <span class="syntax-class">ask</span>(<span class="syntax-annotation">@RequestParam</span> String question) { <span class="syntax-keyword">return</span> aiService.askQuestion(question); } } \` }, service: { explanation: '<h4 class="font-semibold">AIService.java</h4><p class="text-sm text-gray-600 mt-1">This is the central service that orchestrates the RAG pipeline and now also incorporates tool calling via MCP. It retrieves documents, constructs a prompt, and uses Spring AI\\'s \`ToolsAdvisor\` to enable the LLM to call the custom \`FileContentTool\` for dynamic context.</p>', code: \` <span class="syntax-keyword">package</span> com.example.ollamaragapp.service; <span class="syntax-keyword">import</span> org.springframework.ai.chat.ChatClient; <span class="syntax-keyword">import</span> org.springframework.ai.chat.messages.UserMessage; <span class="syntax-keyword">import</span> org.springframework.ai.chat.prompt.Prompt; <span class="syntax-keyword">import</span> org.springframework.ai.chat.prompt.SystemPromptTemplate; <span class="syntax-keyword">import</span> org.springframework.ai.document.Document; <span class="syntax-keyword">import</span> org.springframework.ai.model.function.FunctionCallingOptions; <span class="syntax-keyword">import</span> org.springframework.ai.model.function.FunctionCallbackWrapper; <span class="syntax-keyword">import</span> org.springframework.ai.model.function.FunctionCallbackContext; <span class="syntax-keyword">import</span> org.springframework.ai.vectorstore.SearchRequest; <span class="syntax-keyword">import</span> org.springframework.ai.vectorstore.VectorStore; <span class="syntax-keyword">import</span> org.springframework.beans.factory.annotation.Value; <span class="syntax-keyword">import</span> org.springframework.core.io.Resource; <span class="syntax-keyword">import</span> org.springframework.stereotype.Service; <span class="syntax-keyword">import</span> java.util.List; <span class="syntax-keyword">import</span> java.util.Map; <span class="syntax-keyword">import</span> java.util.stream.Collectors; <span class="syntax-annotation">@Service</span> <span class="syntax-keyword">public class</span> <span class="syntax-class">AIService</span> { <span class="syntax-keyword">private final</span> ChatClient chatClient; <span class="syntax-keyword">private final</span> VectorStore vectorStore; <span class="syntax-keyword">private final</span> FileContentTool fileContentTool; <span class="syntax-comment">// Injected custom tool</span> <span class="syntax-keyword">private final</span> FunctionCallbackContext functionCallbackContext; <span class="syntax-comment">// Required for tool calling</span> <span class="syntax-annotation">@Value</span>(<span class="syntax-string">"classpath:/prompts/qa-system-prompt.st"</span>) <span class="syntax-keyword">private</span> Resource qaSystemPromptResource; <span class="syntax-keyword">public</span> <span class="syntax-class">AIService</span>(ChatClient chatClient, VectorStore vectorStore, FileContentTool fileContentTool, FunctionCallbackContext functionCallbackContext) { <span class="syntax-keyword">this</span>.chatClient = chatClient; <span class="syntax-keyword">this</span>.vectorStore = vectorStore; <span class="syntax-keyword">this</span>.fileContentTool = fileContentTool; <span class="syntax-keyword">this</span>.functionCallbackContext = functionCallbackContext; } <span class="syntax-keyword">public</span> String <span class="syntax-class">askQuestion</span>(String question) { <span class="syntax-comment">// RAG pipeline: Retrieve relevant documents</span> List&lt;Document&gt; docs = vectorStore.similaritySearch( SearchRequest.query(question).withTopK(4) ); String docContent = docs.stream().map(Document::getContent) .collect(Collectors.joining(<span class="syntax-string">"\\\\n"</span>)); SystemPromptTemplate tmpl = <span class="syntax-keyword">new</span> <span class="syntax-class">SystemPromptTemplate</span>(qaSystemPromptResource); Prompt systemPrompt = tmpl.create(Map.of(<span class="syntax-string">"documents"</span>, docContent)); <span class="syntax-comment">// Build ChatClient with tool calling enabled</span> <span class="syntax-keyword">var</span> chatClientWithTools = chatClient.prompt().advisors( <span class="syntax-keyword">new</span> <span class="syntax-class">ToolsAdvisor</span>( <span class="syntax-keyword">new</span> <span class="syntax-class">FunctionCallingOptions</span>(<span class="syntax-string">"getFileContent"</span>), <span class="syntax-comment">// Tell the model about this tool</span> functionCallbackContext ) ).build(); Prompt finalPrompt = <span class="syntax-keyword">new</span> <span class="syntax-class">Prompt</span>(List.of( systemPrompt.getMessages().getFirst(), <span class="syntax-keyword">new</span> UserMessage(question)) ); <span class="syntax-keyword">return</span> chatClientWithTools.call(finalPrompt).getResult().getOutput().getContent(); } } \` }, ingestion: { explanation: '<h4 class="font-semibold">DocumentIngestionService.java</h4><p class="text-sm text-gray-600 mt-1">This service is responsible for loading your .txt files from the resources folder, breaking them into smaller chunks using a \`TokenTextSplitter\`, and then adding them to the \`VectorStore\` for the RAG process.</p>', code: \` <span class="syntax-keyword">package</span> com.example.ollamaragapp.service; <span class="syntax-keyword">import</span> org.springframework.ai.document.Document; <span class="syntax-keyword">import</span> org.springframework.ai.reader.TextReader; <span class="syntax-keyword">import</span> org.springframework.ai.transformer.splitter.TokenTextSplitter; <span class="syntax-keyword">import</span> org.springframework.ai.vectorstore.VectorStore; <span class="syntax-keyword">import</span> org.springframework.beans.factory.annotation.Value; <span class="syntax-keyword">import</span> org.springframework.core.io.Resource; <span class="syntax-keyword">import</span> org.springframework.stereotype.Service; <span class="syntax-keyword">import</span> java.io.IOException; <span class="syntax-keyword">import</span> java.util.Arrays; <span class="syntax-keyword">import</span> java.util.List; <span class="syntax-keyword">import</span> java.util.stream.Collectors; <span class="syntax-annotation">@Service</span> <span class="syntax-keyword">public class</span> <span class="syntax-class">DocumentIngestionService</span> { <span class="syntax-keyword">private final</span> VectorStore vectorStore; <span class="syntax-annotation">@Value</span>(<span class="syntax-string">"classpath:/data/\*.txt"</span>) <span class="syntax-keyword">private</span> Resource\[\] documentResources; <span class="syntax-keyword">public</span> <span class="syntax-class">DocumentIngestionService</span>(VectorStore vectorStore) { <span class="syntax-keyword">this</span>.vectorStore = vectorStore; } <span class="syntax-keyword">public void</span> <span class="syntax-class">ingestDocuments</span>() { List&lt;Document&gt; docs = Arrays.stream(documentResources) .flatMap(r -> { <span class="syntax-keyword">try</span> { <span class="syntax-keyword">return new</span> <span class="syntax-class">TextReader</span>(r).get().stream(); } <span class="syntax-keyword">catch</span> (IOException e) { <span class="syntax-keyword">return</span> java.util.stream.Stream.empty(); } }).collect(Collectors.toList()); TokenTextSplitter splitter = <span class="syntax-keyword">new</span> <span class="syntax-class">TokenTextSplitter</span>(); List&lt;Document&gt; splitDocs = splitter.apply(docs); vectorStore.add(splitDocs); } } \` }, tool: { explanation: '<h4 class="font-semibold">FileContentTool.java</h4><p class="text-sm text-gray-600 mt-1">This is a custom tool that the LLM can call. It simulates reading content from a file system based on the provided file name. In a real application, this would interact with your actual file system or a document management system.</p>', code: \` <span class="syntax-keyword">package</span> com.example.ollamaragapp.service; <span class="syntax-keyword">import</span> org.springframework.ai.tool.Tool; <span class="syntax-keyword">import</span> org.springframework.stereotype.Component; <span class="syntax-annotation">@Component</span> <span class="syntax-keyword">public class</span> <span class="syntax-class">FileContentTool</span> { <span class="syntax-comment">// This method simulates reading content from a file.</span> <span class="syntax-comment">// The @Tool annotation makes this method callable by the LLM.</span> <span class="syntax-annotation">@Tool</span>(<span class="syntax-string">"getFileContent"</span>) <span class="syntax-keyword">public</span> String <span class="syntax-method">getFileContent</span>(String fileName) { <span class="syntax-comment">// In a real application, you would read from your actual file system here.</span> <span class="syntax-comment">// For this example, we return predefined content.</span> <span class="syntax-keyword">if</span> (<span class="syntax-string">"important.txt"</span>.equals(fileName)) { <span class="syntax-keyword">return</span> <span class="syntax-string">"This is very important information for the project."</span>; } <span class="syntax-keyword">else if</span> (<span class="syntax-string">"config.properties"</span>.equals(fileName)) { <span class="syntax-keyword">return</span> <span class="syntax-string">"app.name=MyAIApp\\\\napp.version=1.0"</span>; } <span class="syntax-keyword">else</span> { <span class="syntax-keyword">return</span> <span class="syntax-string">"File not found or content not available for "</span> + fileName; } } } \` }, config: { explanation: '<h4 class="font-semibold">VectorStoreConfig.java</h4><p class="text-sm text-gray-600 mt-1">A simple configuration class that defines the \`VectorStore\` bean. Here, we use \`SimpleVectorStore\`, an in-memory implementation perfect for development and testing. This part remains the same for the RAG aspect.</p>', code: \` <span class="syntax-keyword">package</span> com.example.ollamaragapp.config; <span class="syntax-keyword">import</span> org.springframework.ai.embedding.EmbeddingModel; <span class="syntax-keyword">import</span> org.springframework.ai.vectorstore.SimpleVectorStore; <span class="syntax-keyword">import</span> org.springframework.ai.vectorstore.VectorStore; <span class="syntax-keyword">import</span> org.springframework.context.annotation.Bean; <span class="syntax-keyword">import</span> org.springframework.context.annotation.Configuration; <span class="syntax-annotation">@Configuration</span> <span class="syntax-keyword">public class</span> <span class="syntax-class">VectorStoreConfig</span> { <span class="syntax-annotation">@Bean</span> <span class="syntax-keyword">public</span> VectorStore <span class="syntax-class">vectorStore</span>(EmbeddingModel embeddingModel) { <span class="syntax-keyword">return new</span> <span class="syntax-class">SimpleVectorStore</span>(embeddingModel); } } \` }, prompt: { explanation: '<h4 class="font-semibold">qa-system-prompt.st</h4><p class="text-sm text-gray-600 mt-1">This is a system prompt template that instructs the language model on its role. It defines how the model should use the provided documents (from RAG) and also implies that it can use tools (like \`getFileContent\`) to gather more information if needed to answer the user\\'s question.</p>', code: \` You are a helpful AI assistant. Use the following information (documents) and available tools to answer the user's question. If the answer cannot be found in the provided documents and tools, state that you don't have enough information from the provided context. Do not make up answers. --- Documents: {documents} --- \` } }; // Populate initial content document.getElementById('pom-xml-code').innerHTML = codeData.pom; document.getElementById('properties-code').innerHTML = codeData.properties; document.getElementById('code-explanation').innerHTML = codeData.controller.explanation; document.getElementById('code-display').innerHTML = codeData.controller.code; // Setup Tabs const tabButtons = document.querySelectorAll('.tab-btn'); const tabContents = document.querySelectorAll('\[data-tab-content\]'); tabButtons.forEach(button => { button.addEventListener('click', () => { const tab = button.dataset.tab; tabButtons.forEach(btn => { btn.classList.remove('border-blue-500', 'text-blue-600'); btn.classList.add('border-transparent', 'text-gray-500', 'hover:text-gray-700', 'hover:border-gray-300'); }); button.classList.add('border-blue-500', 'text-blue-600'); button.classList.remove('border-transparent', 'text-gray-500'); tabContents.forEach(content => { if (content.dataset.tabContent === tab) { content.classList.remove('hidden'); } else { content.classList.add('hidden'); } }); }); }); // Code File Viewer const fileButtons = document.querySelectorAll('.code-file-btn'); const codeDisplay = document.getElementById('code-display'); const codeExplanation = document.getElementById('code-explanation'); fileButtons.forEach(button => { button.addEventListener('click', () => { const file = button.dataset.file; const fileData = codeData\[file\]; fileButtons.forEach(btn => { btn.classList.remove('bg-blue-100', 'text-blue-700'); btn.classList.add('hover:bg-stone-100'); }); button.classList.add('bg-blue-100', 'text-blue-700'); button.classList.remove('hover:bg-stone-100'); codeExplanation.innerHTML = fileData.explanation; codeDisplay.innerHTML = fileData.code; }); }); // Mobile Menu const mobileMenuButton = document.getElementById('mobile-menu-button'); const mobileMenu = document.getElementById('mobile-menu'); mobileMenuButton.addEventListener('click', () => { mobileMenu.classList.toggle('hidden'); }); // Active Nav Link on Scroll const sections = document.querySelectorAll('section'); const navLinks = document.querySelectorAll('.nav-link'); const observer = new IntersectionObserver((entries) => { entries.forEach(entry => { if (entry.isIntersecting) { navLinks.forEach(link => { link.classList.remove('active'); if (link.getAttribute('href').substring(1) === entry.target.id) { link.classList.add('active'); } }); } }); }, { rootMargin: '-50% 0px -50% 0px' }); sections.forEach(section => { observer.observe(section); }); }); function copyToClipboard(button) { const codeBlock = button.parentElement; const code = codeBlock.querySelector('code, pre').innerText; navigator.clipboard.writeText(code).then(() => { button.innerText = 'Copied!'; setTimeout(() => { button.innerText = 'Copy'; }, 2000); }).catch(err => { console.error('Failed to copy text: ', err); }); }

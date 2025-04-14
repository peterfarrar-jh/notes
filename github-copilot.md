# Fuel Up Friday - April 2025

# GitHub Copilot

Nikhil Thampi & Vishal Soni  

Overview, demos, and prompt crafting to come...  

New features coming rapidly.  

## GitHub Copilot Overview and Prompt Crafting

### What is GitHub Copilot & How Does It Work?  

AI platform to help fast-track developer productivity.  

Processes questions along with context, analyzes using LLM, and returns suggestions.  

Are you training using our code?  
No. We are using the data only to answer questions; we don't save the code for later use.  

Instead of books and internet searches, use Copilot.  

This is like giving an accountant a calculator.  

Allows focus on business problems, rather than getting sidetracked with syntax, etc.  

#### GitHub Copilot Chat

Ask the bot to explain the code.  

#### Inline Chat
Quickly access Chat inline to ask questions and generate code suggestions.  

### Developer Productivity with Copilot Means Developers Focus on What Matters Most

#### More Time On:

* Designing
* Brainstorming
* Collaborating
* Iterating
* Planning

#### Less Time On:

* Writing tests, repetitive code, boilerplate
* Searching documentation
* Finding vulnerabilities
* Deciphering existing code
* Correcting syntax
* Summarizing changes and comments
* Learning git commands

Three-month project reduced to two and a half weeks.  

## Demo Time

### Extensions

* GitHub Copilot
* GitHub Copilot Chat

Programming language agnostic.  
Supports most popular languages.  

Useful for:

* Greenfield
* Existing
* Migrating
* Test Generation
* Documentation
* Code Review

Example:  
"Create a Jupyter notebook to read the JSON file containing daily sales information. Calculate the sales for each week and store the output data in an MSSQL server table."  

"Explain the code"  
The bot will break down the code and explain what the code does, and what each section of code does.  

"Convert this COBOL to Python"  
Takes about ten seconds to translate. Recommend that you understand what the code is doing, but you won't have to start from scratch.  

"Generate unit tests for this Python code."  
Produces an explanation of what it's doing, then creates the tests.  

"Generate the documentation for the code base."  
Creates detailed documentation. Documentation is based on which files are selected.  

"List vulnerabilities in the code."  
"Show the code after it is fixed for these issues."  
"Optimize this code for..."  

"Create a TSQL procedure to read the marketing ad table containing ad details for each product and calculate the return on marketing amount by joining the above tables with daily sales data. Identify the top 3 products which are giving better ..."  

"Create a Terraform template for AWS."  

"Generate my diagram in Mermaid for markdown."  

Images (screenshots) can be used as context for Copilot. Drag and drop an image into the chat.  

`@workspace` tells Copilot to use all open files.  

`#file:` followed by the filename will focus Copilot on just that file.  

## Prompt Crafting

### What's Prompt Crafting?

**Prompt crafting**: the process of giving clear natural language instructions to computer programs, such as the large language models (LLMs) that drive GitHub Copilot functionalities.  

Illustration:  
"Create a calculator class" vs. "Create a calculator class which can generate sin, cos, and tan in addition to regular calculator functions. The code should be in Java."  

Ambiguous instructions will result in a lot of assumptions on the part of the agent.  

You can select different models in the Copilot chat.  

### Pillars of Effective Copilot Prompts

* **Context** - Information provided in the prompt that helps Copilot understand the task better.
* **Intent** - The specific goal or purpose you have in mind when creating a prompt.
* **Clarity** - The quality of being unambiguous and easy to understand.
* **Specificity** - The level of detail and precision in a prompt.

### Context is Key

Copilot relies on both the underlying model and the context in your editor to provide high-quality suggestions.

* Code completion prioritizes the immediate context, as well as context found in open files.
* Chat has the ability to bring in even more context.

### Copilot is Probabilistic, Not Deterministic

Copilot LLMs are sophisticated probability engines, so you might get different results for the same question.  

Copilot doesn't store your information or its answers.  

### Use Copilot's Code Completion To...

### Use Copilot Chat To...

* Open-ended questions.
* Use slash commands to invoke capabilities that may not be possible or may require several steps if you use natural language.

### Best Practices

**Variable Names:** Use descriptive variable names to make your intentions clear.  

**Method Signatures:** Define method signatures with unambiguous parameters and names.  

**Naming Conventions:** Use conventions.  

### Ask Chat for Help in Refactoring

**Input/Output Format:** Describe expected input and output formats.  

**Error Handling:** Specify error handling scenarios.  

**Control Structures:** Describe control flow structures.  

Include a high level of description of your requirements at the top of your file or in your chat thread.  
This is especially complemented by following up with specific instructions in the form of steps.  

Provide examples in your prompts to clarify expectations.  

```
Please consider the following example data:
Example 1: [5, 10, 15, 20, 8]
Example 2: [2, 15, 32, 200, 208]
```

Keep files open in your project folder that are relevant to the requirements of your current file and leverage them.  

Use the `#` symbol to reference a chat variable. With `#file` you can pass the contents of a file in the workspace to Copilot.  

### /Slash Commands

* `/explain`  
* `/tests`  
* `/fix`  
* `@workspace`  
* `/help`  

### If At First You Don't Succeed, Iterate!

**Initial Prompt:** Lay out the basic idea.  
**Second Prompt:** Give more details.  

Note:  
Find the GitHub Copilot documentation.  
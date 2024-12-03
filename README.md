# Ticketing Service AI Chatbot with DST

## Overview 
This project focuses on developing a Train Ticketing AI Chatbot powered by mistral leveraging Dialog State Tracking (DST) to provide an intelligent, user-friendly interface for train ticket booking. The chatbot utilizes the MultiWOZ 2.2 dataset, a rich dataset for conversational AI tasks, to train its conversational capabilities. The primary components of the project include:

- **Dataset Loading and Exploration:**

The chatbot is trained on the MultiWOZ 2.2 dataset, which includes structured dialogue data tailored for real-world scenarios like ticket booking.

- **Integration with LLMs (Large Language Models):**

The chatbot interfaces with Mistral, hosted on Ollama, to leverage advanced transformer-based capabilities for natural language understanding and generation.

- **Dialog State Management:**

The project implements robust Dialog State Tracking (DST), enabling the chatbot to understand and remember the user’s intent and preferences during multi-turn conversations. It also maintains a record of chat history, ensuring continuity in the dialogue and allowing the chatbot to reference previous interactions for better context and accuracy.

- **Entity Recognition and Intent Detection:**

Using regular expressions and classification mechanisms, the chatbot extracts entities like train destinations, dates, and times while detecting user intent (e.g., ticket inquiry or cancellation).

- **Evaluation of Chatbot Performance:**

The chatbot's responses are evaluated on metrics such as BLEU score, dialogue success rate, and match rate to ensure its effectiveness and usability.

## Dialogue State Tracking (DST)
Dialog State Tracking (DST) is a core component of task-oriented dialogue systems, designed to manage and maintain the conversation context across multiple turns of interaction. In these systems, the chatbot interacts with users to accomplish specific tasks, such as booking tickets, ordering food, or answering queries.

DST's primary function is to track and update the dialogue state—a structured representation of the user's preferences, intents, and relevant information gathered during the conversation. The dialogue state typically includes entities (e.g., departure city, destination city, date) and the user's intent (e.g., booking a ticket, modifying an order).

**_Key Features of DST:_**
- Context Management:
  DST keeps track of the conversation history to maintain continuity, ensuring the chatbot can provide accurate and relevant responses.
- Dynamic Updates:
  As new information is provided by the user, DST updates the state in real-time.
- Task-Specific Focus:
  DST helps the chatbot focus on extracting information necessary to fulfill the task, ignoring irrelevant details.

**_Example of Dialog State Tracking (DST):_**

In a multi-turn conversation, DST tracks the user's inputs and updates the state to maintain context. Here's a simplified example:

- User: "I want to book a train ticket from Nashville to Chicago."
- Chatbot's Internal State (Updated):
```
  {
  "departure_city": "Nashville",
  "destination_city": "Chicago",
  "date": null,
  "intent": "book_ticket"
  }
```
- User: "I want to travel next Monday."
- Chatbot's Internal State (Updated):
```
  {
  "departure_city": "Nashville",
  "destination_city": "Chicago",
  "date": "2024-12-04",
  "intent": "book_ticket"
  }
```
- Chatbot: "I’ve found trains from Nashville to Chicago on Monday, December 4th. Would you like me to book one?"

DST ensures the chatbot remembers the user's preferences (e.g., departure and destination cities) across multiple turns and updates dynamically with new information (e.g., travel date).

## Model
Mistral is a state-of-the-art transformer-based large language model (LLM) designed for efficient and high-performance natural language processing (NLP) tasks. Developed by Mistral AI, Mistral models, such as Mistral 7B, represent a new generation of open-weight LLMs that optimize performance and scalability. Furthermore, it is hosted on Ollama, which enhanced the accessibility to use on local machine.

Link to mistral model: https://ollama.com/library/mistral

### Key features of Mistral include:

- Compact yet Powerful:
With only 7 billion parameters, Mistral achieves competitive performance compared to larger models by leveraging advanced techniques such as Grouped-Query Attention (GQA) for better memory and computation efficiency.

- Decoder-Only Architecture:
Mistral employs a decoder-only transformer architecture, making it well-suited for tasks involving text generation, such as dialogue systems, summarization, and code completion.

- Open-Weight Accessibility:
Mistral is available with open weights, making it a cost-effective and flexible choice for research and development in various NLP applications.

- Highly Optimized Training:
It incorporates innovations in model training, such as balanced datasets and efficient use of compute resources, resulting in a model that excels at real-world tasks.

### Reason for choosing Mistral
The choice of Mistral for the Train Ticketing AI Chatbot project is driven by several compelling reasons:
- Efficiency and Performance:
Mistral’s compact size and optimized architecture allow it to perform efficiently on tasks like Dialog State Tracking (DST), making it suitable for real-time conversational applications.
- Open-Weight Accessibility:
The open-weight nature of Mistral allows customization and fine-tuning, enabling us to adapt the model for the specific domain of train ticket booking without high costs or licensing restrictions.
- Transformer-Based Excellence:
As a transformer model, Mistral excels at handling contextual and sequential data, critical for maintaining conversation history and understanding user intent in multi-turn dialogues.
- Ease of Integration:
Mistral’s compatibility with modern NLP frameworks and APIs (e.g., Ollama) simplifies its deployment in projects, ensuring smooth integration with the chatbot’s backend.
- Cost-Effective Scalability:
Mistral balances performance with resource efficiency, providing high-quality outputs without the computational demands of larger models like GPT-3 or GPT-4.

By choosing Mistral, the project benefits from a cutting-edge model that is both powerful and adaptable, ensuring a robust and efficient chatbot capable of meeting user needs effectively.

## Dataset

The MultiWOZ (Multi-Domain Wizard-of-Oz) dataset is a large-scale, multi-domain dialogue dataset containing conversations between users and systems across various domains, such as restaurant booking, train scheduling, and hotel reservations. It is widely used for training and evaluating conversational agents, particularly in multi-domain dialogue state tracking. The dataset is available through Hugging Face Datasets and other academic repositories, with permissions allowing non-commercial academic use, provided users adhere to the dataset license. Preprocessing scripts for MultiWOZ are included in the project notebook, enabling seamless integration into the training pipeline.

## Critical Analysis

### Impact
This project showcases the potential of AI in automating and optimizing ticketing services, reducing the workload of human operators while offering a seamless user experience. The chatbot can efficiently handle multi-turn conversations and adapt to user needs in real time, paving the way for advancements in customer service automation.

### Results
The chatbot demonstrates strong performance, highlighting its effectiveness in managing dialogue state tracking across various scenarios. Its ability to provide accurate and context-aware responses enhances the user experience, showcasing its potential for real-world applications. However, challenges remain, particularly in handling ambiguous user inputs and out-of-domain queries, which present opportunities for further refinement.

### Next Steps
Moving forward, the next steps involve deploying the chatbot on real-world ticketing platforms to gather user feedback and evaluate its performance under practical conditions. To enhance its capabilities, exploring advanced transformer models like GPT-4 or fine-tuning the existing architecture for better domain-specific adaptation is recommended. Additionally, scalability efforts should focus on expanding the chatbot to handle more domains and integrating external APIs for real-time ticket booking functionality.

## Resource links 
* Quick Links to related papers
	* [Chain of Thought Explanation for Dialogue State Tracking](https://arxiv.org/abs/2403.04656)
 	* ["Do you follow me?": A Survey of Recent Approaches in Dialogue State Tracking](https://arxiv.org/abs/2207.14627)
  	* [Learning to Ask Questions for Zero-shot Dialogue State Tracking](https://core.ac.uk/outputs/591216830/?source=2)
 	* [Recurrent Polynomial Network for Dialogue State Tracking](https://core.ac.uk/outputs/559990324/?source=2)
* Relevant blog posts
  * [Dialogue State Tracking](https://paperswithcode.com/task/dialogue-state-tracking)
  * [Mastering Dialogue Systems: Fine-tuning GPT for Dialogue State Tracking and Dialogue Management](https://30dayscoding.com/blog/fine-tuning-gpt-for-dialogue-state-tracking-and-dialogue-management?srsltid=AfmBOop8ZwFd63bDhxO11zuQHZ8R0YCzrblyrhg0Z0XNMownPJ-6ZSM6)




![](Images/figure1_1.png)

![](Images/figure1_2.png)

**Question 1**

_**In DecodingTrust, one of the evaluation criteria is 'out-of-distribution robustness.' Why is this aspect crucial for assessing the trustworthiness of GPT models?**_

- **Guiding Responsible Deployment of LLMs:**

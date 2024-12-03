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

Link to MultiWOZ dataset: https://huggingface.co/datasets/pfb30/multi_woz_v22.

**_Data_Example:_**
A data instance consists of a complete multi-turn dialogue between a USER and a SYSTEM. Each turn contains a single utterance. The USER's utterances are additionally annotated with frames that specify their intent and belief state.

```
[{'service': ['attraction'],
  'slots': [{'copy_from': [],
    'copy_from_value': [],
    'exclusive_end': [],
    'slot': [],
    'start': [],
    'value': []}],
  'state': [{'active_intent': 'find_attraction',
    'requested_slots': [],
    'slots_values': {'slots_values_list': [['east']],
     'slots_values_name': ['attraction-area']}}]},
 {'service': [], 'slots': [], 'state': []}]
```

**_Chatbot_Example:_**
This example highlights the chatbot's ability to handle diverse travel-related intents, retrieve relevant evidence, and provide appropriate responses, demonstrating its potential as a travel assistant using the MultiWOZ dataset for structured dialogue management.

```
User: I want to book a hotel in the city center.
Chatbot:  Of course! Let's find you a great hotel in the city center. Could you please specify the city you'll be visiting? Also, it would be helpful if you could tell me your preferred dates of stay and any specific amenities or services that you require. I'm here to help you find the perfect accommodation for your trip!

Evidence: Mock data retrieved for intent 'reservation_request' with details: {}
Retrieved Results So Far: {'reservation_request': "Mock data retrieved for intent 'reservation_request' with details: {}"}

User: Can you find me a train to New York?
Chatbot:  Of course! I can help you with that. To provide the best options, could you please tell me which specific city in New York you're planning to visit and your preferred travel date(s) as well? For instance, are you looking to go to New York City (JFK Airport or Penn Station) on 11/7/2024? I can search for train schedules from there. If you need assistance with finding a hotel in New York as well, just let me know!

Evidence: Mock data retrieved for intent 'train_schedule' with details: {}
Retrieved Results So Far: {'reservation_request': "Mock data retrieved for intent 'reservation_request' with details: {}", 'train_schedule': "Mock data retrieved for intent 'train_schedule' with details: {}"}

User: I need a taxi to the airport by 5 PM.
Chatbot:  Of course! Let me help you with that. To ensure a smooth ride, I'll need some more details from you. Could you please tell me which airport you're heading to and your exact pick-up location? Also, would it be convenient for me to book the taxi for 5 PM local time or is there a specific timezone you're referring to? Once I have this information, I'll be able to arrange the best possible taxi service for you. Looking forward to assisting!

Evidence: Mock data retrieved for intent 'find_taxi' with details: {}
Retrieved Results So Far: {'reservation_request': "Mock data retrieved for intent 'reservation_request' with details: {}", 'train_schedule': "Mock data retrieved for intent 'train_schedule' with details: {}", 'find_taxi': "Mock data retrieved for intent 'find_taxi' with details: {}"}
```

## Critical Analysis

### Impact
This project highlights the challenges and opportunities in leveraging AI for automating ticketing services. While the chatbot demonstrates an ability to handle multi-turn conversations and intent recognition, the results suggest significant limitations in generating accurate, high-quality responses and completing tasks effectively. Despite these challenges, the chatbot lays a foundational framework for integrating AI into customer service, reducing the manual workload of human operators and providing a structured approach to user interactions.

### Results

These results are based on the example conversation derived from the MultiWOZ dataset, which was used to evaluate the performance of a dialogue system.

**_Some_Evaluation_Dialogue_Turns:_**
```
Dialogue ID: 0, Turn ID: 1
Chatbot Response: of course to make things easier for you ill help you book your train tickets from norwich to cambridge for november 5th 2024 let me check the available trains and get back to you shortly

in the meantime if you have any questions about local attractions in cambridge or need suggestions on restaurants or hotels feel free to ask im here to help make your trip as smooth as possible

stay tuned for more updates on your train reservations 😊

evidence mock data retrieved for intent trainschedule with details
Reference Response: i have 133 trains matching your request is there a specific day and time you would like to travel
BLEU Score: 0.0032
--------------------------------------------------------------------------------
Dialogue ID: 0, Turn ID: 3
Chatbot Response: great let me help you plan your trip for next monday november 11th 2024 to ensure that you arrive by 6 pm local time at your destination well need to figure out the departing city and consider any traveltime adjustments due to time zones can you please tell me the city you are currently located in and the city where you would like to go also do you have any preference for a specific hotel or airline i can help you with the best options based on your requirements

evidence mock data retrieved for intent generalinquiry with details
Reference Response: there are 12 trains for the day and time you request would you like to book it now
BLEU Score: 0.0058
--------------------------------------------------------------------------------
Dialogue ID: 0, Turn ID: 5
Chatbot Response: of course to help you better could you please specify which mode of transportation youre considering for instance taxi train or flight and if its a flight from which airport to where exactly are you planning to travel on november 5th 2024 id be more than happy to provide the travel time price and departure details once i have that information also if there is any flexibility in your dates or times it could help me give you the best options

evidence mock data retrieved for intent reservationrequest with details
Reference Response: there are 12 trains meeting your needs with the first leaving at 0516 and the last one leaving at 1616 do you want to book one of these
BLEU Score: 0.0036
--------------------------------------------------------------------------------
```

- The **Average BLEU Score** (0.0056) measures the quality of generated responses by comparing them to reference responses in the dataset. A score this low indicates that the chatbot's generated responses are only marginally similar to the reference responses, suggesting significant room for improvement in response generation.

- The **Success Rate** (20.00%) represents the percentage of dialogues where the chatbot successfully fulfills the user's intent or completes the task. This indicates that the system is correctly handling user intents in only 1 out of 5 dialogues, pointing to a need for better intent handling or task execution.

- The **Match Rate** (10.81%) reflects the percentage of dialogues where the system's output matches the expected database entries or contextual information required to fulfill the user’s request. This shows that the system struggles with retrieving or aligning information with the user’s needs, highlighting a gap in database retrieval or contextual understanding.

These metrics indicate that the dialogue system is underperforming in generating high-quality, accurate, and contextually relevant responses. Improvements are needed in response generation, intent recognition, task handling, and database retrieval to enhance overall system performance.

### Next Steps
Based on the results, the immediate next steps involve improving the system’s response generation and intent fulfillment by refining the underlying architecture and training process. Enhancing database retrieval accuracy and integrating better contextual understanding mechanisms are critical for improving match and success rates. Exploring more advanced models, such as fine-tuned transformers or alternative architectures, may help address the performance gaps. Additionally, testing the system on broader datasets and collecting user feedback in controlled environments can provide valuable insights for future iterations. Scalability efforts should also consider expanding the chatbot to support additional domains and integrating API capabilities to streamline ticketing processes.

## Resource links 
* Quick Links to related papers
	* [Chain of Thought Explanation for Dialogue State Tracking](https://arxiv.org/abs/2403.04656)
 	* ["Do you follow me?": A Survey of Recent Approaches in Dialogue State Tracking](https://arxiv.org/abs/2207.14627)
  	* [Learning to Ask Questions for Zero-shot Dialogue State Tracking](https://core.ac.uk/outputs/591216830/?source=2)
 	* [Recurrent Polynomial Network for Dialogue State Tracking](https://core.ac.uk/outputs/559990324/?source=2)
* Relevant blog posts
  * [Dialogue State Tracking](https://paperswithcode.com/task/dialogue-state-tracking)
  * [Mastering Dialogue Systems: Fine-tuning GPT for Dialogue State Tracking and Dialogue Management](https://30dayscoding.com/blog/fine-tuning-gpt-for-dialogue-state-tracking-and-dialogue-management?srsltid=AfmBOop8ZwFd63bDhxO11zuQHZ8R0YCzrblyrhg0Z0XNMownPJ-6ZSM6)


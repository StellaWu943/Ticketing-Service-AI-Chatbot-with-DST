# Ticketing Service AI Chatbot with DST

## Overview 
In recent years, large language models (LLMs) like GPT-3.5 and GPT-4 have demonstrated impressive capabilities, leading to their consideration for use in high-stakes areas such as 
![](Images/figure1_1.png)

![](Images/figure1_2.png)

## Model
mistral model card

## MultiWOZ Dataset

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





**Question 1**

_**In DecodingTrust, one of the evaluation criteria is 'out-of-distribution robustness.' Why is this aspect crucial for assessing the trustworthiness of GPT models?**_

- **Guiding Responsible Deployment of LLMs:**

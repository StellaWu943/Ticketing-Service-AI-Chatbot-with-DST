# Service AI Chatbot with DST

## Overview 
In recent years, large language models (LLMs) like GPT-3.5 and GPT-4 have demonstrated impressive capabilities, leading to their consideration for use in high-stakes areas such as healthcare, finance, and customer service. However, these models face significant trustworthiness challenges, particularly regarding the handling of sensitive information, bias mitigation, and maintaining ethical responses. Despite recent improvements, there is limited comprehensive research on the trustworthiness of these models, which is crucial for their safe and responsible deployment in real-world applications.

This paper addresses the need for a robust evaluation of LLM trustworthiness across multiple dimensions essential for safe and ethical deployment. The authors introduce a comprehensive benchmark called DecodingTrust, which evaluates eight trustworthiness dimensions: toxicity, stereotype bias, adversarial robustness, out-of-distribution robustness, robustness against adversarial demonstrations, privacy, machine ethics, and fairness. Each dimension presents unique challenges, as LLMs are still susceptible to generating harmful, biased, or unethical outputs, especially when exposed to adversarial prompts or ambiguous contexts. Existing benchmarks often focus narrowly, leaving a gap in understanding how models perform across this broader trustworthiness spectrum.

The eight dimensions in DecodingTrust include:

- Toxicity: Assessing the models' propensity to generate harmful or offensive content.
- Stereotype Bias: Evaluating the presence of biased outputs related to societal stereotypes.
- Adversarial Robustness: Testing the models' resilience against inputs designed to deceive or manipulate them.
- Out-of-Distribution Robustness: Measuring performance on inputs that differ from the training data.
- Robustness on Adversarial Demonstrations: Analyzing susceptibility to misleading examples during in-context learning.
- Privacy: Investigating the potential for models to leak sensitive information from training data or user interactions.
- Machine Ethics: Evaluating adherence to ethical guidelines in decision-making processes.
- Fairness: Ensuring equitable treatment across different demographic groups.

![](Images/figure1_1.png)

![](Images/figure1_2.png)


To evaluate these dimensions, the authors crafted custom datasets and prompt designs tailored to each area, creating scenarios that stress-test the models with adversarial, misleading, or ethically - challenging inputs. For instance, in assessing toxicity, they used both standard and challenging prompts specifically designed to elicit harmful responses. For stereotype bias, they examined the models' responses to statements containing embedded stereotypes and measured the likelihood of generating biased or stereotypical outputs.

Systematic tests were conducted on GPT-3.5 and GPT-4 using the DecodingTrust benchmark across all eight dimensions. Key findings revealed that, while GPT-4 generally performs better than GPT-3.5 in standard benchmarks, it is more vulnerable to adversarial manipulation, especially through "jailbreaking" prompts. Such prompts circumvent content filters by exploiting GPT-4's enhanced instruction-following capabilities, leading to higher susceptibility to biased content and privacy leaks under carefully crafted prompts.

The study provided both quantitative and qualitative insights into the limitations of these models, identifying cases where they failed to respond safely or ethically. These findings highlight the need for more robust safeguards and model design improvements to enhance resilience against adversarial scenarios while maintaining high trustworthiness standards.


**Question 1**

_**In DecodingTrust, one of the evaluation criteria is 'out-of-distribution robustness.' Why is this aspect crucial for assessing the trustworthiness of GPT models?**_

Out-of-distribution (OOD) robustness is critical for trustworthiness because real-world applications frequently expose language models to inputs or contexts that differ from those encountered during training. In these cases, a trustworthy model should recognize its limitations, avoid generating confident but inaccurate answers, and ideally respond with uncertainty or a disclaimer if it doesn’t "know" the answer. Failure in OOD robustness can lead to responses that are confidently incorrect, misleading users in high-stakes environments like healthcare, law, or finance.

***How did the authors evaluate Out-of-Distribution Robustness to uncover vulnerabilities in GPT-3.5 and GPT-4:***

The authors of DecodingTrust assessed OOD robustness by presenting GPT-3.5 and GPT-4 with prompts that included unfamiliar language styles (e.g., Shakespearean) and queries about recent events beyond the models' training data. They found that while GPT-4 was generally better at handling unfamiliar styles and could sometimes respond with "I don’t know" for recent events, it still occasionally "hallucinated" answers or gave made-up responses. This vulnerability suggests that while GPT-4 has improved in handling certain OOD prompts, it still requires enhancements in recognizing and managing unknown or out-of-scope inputs to be truly reliable in diverse real-world applications.

**Question2**

**What makes GPT-4 more vulnerable to generating toxic or biased outputs in adversarial contexts compared to GPT-3.5, and what specific prompt types can lead to such behaviors?**

***Key Reasons for GPT-4’s Increased Vulnerability:***

- **Enhanced Instruction Following:** 
  - GPT-4 has improved capabilities to follow instructions precisely, which is beneficial for most tasks but makes it more susceptible to adversarial prompts that guide it toward toxic or biased outputs.
  - *Because GPT-4 is better at following instructions, it is more likely to produce harmful outputs if prompted with carefully crafted, misleading instructions.*

- **Sensitivity to Adversarial Prompts:**
  - The paper shows that GPT-4 responds to certain adversarial prompt types—like “role-playing” or “straightforward instructions” that bypass content filters—by following them more rigorously than GPT-3.5.
  - This increased sensitivity makes it easier for adversaries to manipulate GPT-4 into generating undesirable content.

- **Complex Prompt Interpretation:** 
  - GPT-4 can interpret complex prompts with intricate context, which inadvertently makes it more responsive to nuanced adversarial instructions that encourage biased or toxic content.

### Supporting Figures from the Paper

- **Figure 2: *Examples of Undesirable Responses of GPT-4 Given Adversarial System Prompts***
![Figure 2: Examples of Undesirable Responses of GPT-4 Given Adversarial System Prompts](Images/Figure2.png)
  - This figure showcases specific examples where adversarial prompts lead GPT-4 to produce toxic or offensive content.

- **Figure 7: *Toxicity of GPT-3.5 and GPT-4 Given Diverse System Prompts***
![Figure 7: Toxicity of GPT-3.5 and GPT-4 Given Diverse System Prompts](Images/Figure7.png)
  - This figure compares the average toxicity scores for GPT-3.5 and GPT-4 across various adversarial prompts.
  - It highlights that GPT-4 has consistently higher toxicity scores than GPT-3.5, especially when straightforward or role-playing prompts are used.


## DecodingTrust intersection with model training and model use

**Intersection with Model Training**

The training methodology of GPT models, specifically the use of vast datasets that include diverse language patterns and content types, contributes significantly to trustworthiness issues. DecodingTrust highlights that despite the extensive data used, models can still produce biased, toxic, or privacy-violating outputs under specific conditions. This is partly because the pretraining datasets are so large and varied that they inevitably contain biased and potentially harmful content. Even with RLHF fine-tuning, which is intended to mitigate such outputs, the paper finds that GPT-4, in particular, can still be led to reproduce these biases and toxic patterns, especially under adversarial prompting.

Moreover, the in-context learning capabilities of GPT-3.5 and GPT-4—where models adapt to few-shot demonstrations provided within a prompt—introduce new risks when these demonstrations are adversarially crafted. For example, misleading in-context demonstrations can skew model outputs toward producing biased or otherwise untrustworthy content. This reveals a limitation in the model's training approach, as it lacks sufficient safeguards against adversarial in-context learning scenarios, which could be mitigated by additional fine-tuning on adversarially crafted demonstrations or by introducing robust in-context learning defenses.

**Intersection with Model Use and Deployment**

The findings in DecodingTrust intersect significantly with practical concerns surrounding the deployment of GPT models, especially in high-stakes and sensitive applications. The use of these models in domains such as healthcare, finance, and customer service implies that any biases, toxic responses, or privacy breaches could have severe consequences. The paper demonstrates that the current trustworthiness mechanisms are insufficiently robust against well-crafted adversarial inputs, which raises serious concerns for their use in critical real-world applications.

For instance, the paper’s analysis of GPT-4’s susceptibility to “jailbreaking” prompts underlines a need for stricter prompt filtration and user-access control in deployment settings. Without such controls, GPT models could be manipulated to generate unsafe content despite embedded safety constraints. Additionally, the paper’s findings on privacy leakage imply that model deployment in contexts where sensitive data is processed should involve privacy-preserving mechanisms such as differential privacy or restricted response generation when handling confidential information. These findings highlight that achieving trustworthiness in model use requires a holistic approach that integrates secure prompt handling, enhanced privacy safeguards, and situational awareness regarding the model's limitations in ethical reasoning and fairness.

## Critical Analysis

### Areas Overlooked or Underdeveloped

- **Limited Exploration of Defense Mechanisms:**
  - While the paper excels in identifying key trustworthiness vulnerabilities in GPT models, it leaves an important gap in actionable defenses or mitigation strategies that could reduce these risks. Given the potential real-world implications of model misuse in sensitive fields such as healthcare and finance, the absence of in-depth discussions on countermeasures is notable.
  - The authors could have explored a range of defenses, such as advanced prompt filtering, model fine-tuning, or reinforcement techniques aimed specifically at hardening the model against adversarial inputs. For example, defenses like adversarial training (exposing models to adversarial prompts during training) or content filtering post-generation could help mitigate some of the vulnerabilities highlighted in the study. These practical, actionable measures would contribute significantly to making GPT-4 more robust in real-world settings.

- **Lack of Real-World Application Scenarios:**
  - The study is primarily centered on synthetic, highly controlled adversarial prompts, but it does not discuss how frequently such prompts are likely to appear in real-world applications. This is a crucial limitation, as understanding the likelihood of encountering adversarial prompts would clarify the practical risk posed by these vulnerabilities.
  - Incorporating a discussion on realistic application scenarios would have added depth to the paper’s findings. For instance, examining the behavior of GPT-4 in common use cases like customer service, educational tools, or content moderation could highlight when and where the risks of toxic or biased outputs are most likely to arise. This would better contextualize the findings for stakeholders and developers who are considering deploying these models in high-stakes environments.

- **Insufficient Analysis of Contextual Nuances in Bias:**
  - The paper takes important steps in assessing bias across demographic groups, yet it does not delve into the potential impact of cultural or linguistic nuances on bias outcomes. Bias can vary significantly based on regional, cultural, or linguistic contexts, and failing to consider these factors can oversimplify the complexity of the issue.
  - For a more comprehensive evaluation, a granular approach—such as testing how GPT models respond to culturally specific or regionally relevant prompts—could provide valuable insights. This would be particularly useful for understanding how models may inadvertently reinforce stereotypes in specific populations, adding another layer of depth to the bias analysis.

### Potential for Further Development

- **In-depth Comparison with Non-GPT Models:**
  - The paper’s focus on comparing GPT-3.5 and GPT-4 yields valuable insights but limits understanding by excluding other prominent large language models (LLMs) like Google’s PaLM or Anthropic’s Claude, which may have different architectures or training methods and could exhibit distinct trustworthiness profiles.
  - A broader comparison with these models could deepen the findings, offering a more holistic view of GPT-4’s relative trustworthiness. This would not only contextualize GPT’s performance within the broader LLM landscape but also help clarify if its vulnerabilities are unique or common across models. By situating GPT-4’s results alongside those of other LLMs, the study would better serve researchers and practitioners looking to select or develop safer and more robust AI models.

- **Exploration of the Role of Reinforcement Learning from Human Feedback (RLHF):**
  - The paper briefly mentions that GPT-4’s heightened instruction-following ability is a result of Reinforcement Learning from Human Feedback (RLHF), yet it doesn’t thoroughly examine how RLHF itself might inadvertently contribute to biases or toxic responses. This leaves room for further analysis, as RLHF aims to align models with human values but may also reinforce unwanted patterns if not carefully managed.
  - An in-depth examination of RLHF’s influence on both beneficial and undesirable behaviors would enhance understanding of GPT-4’s alignment and response tendencies. For example, analyzing how the RLHF process might introduce or amplify biases due to the nature of feedback could provide critical insights for refining training methodologies. This focus would help practitioners optimize RLHF’s implementation, creating models that align with human values more effectively and with reduced risk of harmful outputs.


## Impacts

### Impact of the Work on the AI Landscape

- **Elevating Standards for Trustworthiness in AI:**
  - This paper makes a significant contribution by establishing a comprehensive benchmark for evaluating trustworthiness in large language models (LLMs). It brings together multiple dimensions of trustworthiness, such as toxicity, bias, privacy, adversarial robustness, machine ethics, and fairness, all under a unified framework.
  - By setting a high standard for trustworthiness evaluation, this work encourages AI practitioners and developers to prioritize ethical and safety considerations alongside model performance, pushing the boundaries of responsible AI practices.

- **New Perspectives on GPT-4’s Capabilities and Vulnerabilities:**
  - The study’s deep dive into GPT-4’s trustworthiness, particularly its susceptibilities to toxic or biased outputs under adversarial conditions, reshapes how researchers and developers perceive the model’s limitations. This nuanced understanding of GPT-4’s vulnerabilities can inform responsible deployment, especially in sensitive areas like healthcare, finance, and customer service, where trustworthiness is critical.
  - It has also helped redirect attention to the duality of instruction-following improvements in GPT-4: while enhancing usefulness, it also increases the potential for harm when exposed to adversarial manipulation. This insight is now a focal point in ongoing discussions on model alignment and robustness.

- **Influencing Future Research on Defense Mechanisms:**
  - The paper’s identification of specific adversarial strategies that can induce toxic or biased outputs in GPT-4 is likely to spur research into countermeasures and defense mechanisms. Areas like adversarial training, enhanced prompt filtering, and reinforcement learning techniques are becoming key topics as researchers work to address the vulnerabilities highlighted by this study.
  - This work has likely laid the groundwork for developing improved safeguards in LLMs, accelerating research into methods to mitigate biases, toxicity, and privacy risks without compromising model usability.

### Intersection with Other Work (Past, Present, and Future)

- **Building on Previous Work in Model Evaluation:**
  - Prior to this study, benchmarks like GLUE and SuperGLUE mainly focused on model accuracy and language understanding. More recent benchmarks, such as AdvGLUE and HELM, have expanded to include robustness and bias but often lacked a complete, trustworthiness-focused approach.
  - This paper builds on these foundational works by integrating a broader spectrum of trustworthiness metrics, making it one of the most holistic evaluations of GPT models to date. It sets a new benchmark for the field, requiring future work on model evaluation to consider a similarly comprehensive scope.

- **Addressing Contemporary Concerns in AI Ethics and Safety:**
  - As society becomes increasingly reliant on AI, ethical concerns such as bias, fairness, and privacy have moved to the forefront of AI research. This study addresses these critical concerns by empirically demonstrating where GPT-4 succeeds and where it falters under trustworthiness metrics, offering a data-driven approach to AI ethics.
  - By exposing the risks of deploying LLMs without rigorous safeguards, this paper intersects with ongoing policy and regulatory discussions on AI transparency, ethical use, and accountability. The findings underscore the need for clear standards and guidelines in AI governance, impacting both technological development and regulatory frameworks.

- **Catalyzing Future Research on Robustness and Safety in LLMs:**
  - This work is likely to shape the future of AI safety research by inspiring further exploration into model alignment and defense against adversarial attacks. Future studies may extend the work by creating more nuanced adversarial prompts, building layered defense systems, and developing better model tuning methods to enhance both alignment and robustness.
  - The evaluation framework presented could serve as a foundation for assessing next-generation models, such as GPT-5 or new releases of open LLMs. As models become increasingly integrated into societal functions, the benchmarks set by this paper may guide ongoing innovations in safe and ethical AI design.

### Importance of the Work

- **Guiding Responsible Deployment of LLMs:**
  - The paper’s findings have immediate implications for practitioners deploying LLMs in sensitive domains. By outlining specific trustworthiness weaknesses in GPT-4, it serves as a caution for developers to carefully consider the safety protocols and context in which these models are deployed.
  - Organizations can use insights from this paper to evaluate whether GPT-4 or similar models meet their ethical and safety requirements, influencing their model selection, deployment, and post-deployment monitoring practices.

- **Pioneering a Comprehensive Trustworthiness Benchmark:**
  - This paper’s establishment of an all-encompassing trustworthiness benchmark fills a critical gap in LLM research, offering a systematic approach to evaluating model safety. It not only adds to the body of research on LLM trustworthiness but also provides a replicable evaluation framework that can be applied to emerging models.
  - By addressing multiple aspects of trustworthiness, this benchmark may become a standard for evaluating AI models moving forward, helping to align industry practices with ethical AI standards.

In summary, this paper significantly impacts AI research by broadening the lens through which we evaluate LLMs, setting the stage for more responsible and transparent AI. Its focus on trustworthiness and model vulnerabilities encourages a shift towards safer, ethically aligned AI development, likely influencing both the direction of future research and the standards of model deployment.

## Resource links 
* This repository is forked from the [original repository](link)
* Quick Links to related papers
	* [A Survey of GPT-3 Family Large Language Models Including ChatGPT and GPT-4](https://arxiv.org/abs/2310.12321)
 	* [Robustness Over Time: Understanding Adversarial Examples' Effectiveness on Longitudinal Versions of Large Language Models](https://arxiv.org/abs/2308.07847)
  * [https://github.com/microsoft/LoRA](https://arxiv.org/abs/2311.16101))
 	* [Trustworthy LLMs: a Survey and Guideline for Evaluating Large Language Models' Alignment](https://arxiv.org/abs/2308.05374)
* Relevant blog posts and videos
  * [GPT-3.5 and GPT-4 comparative analysis](https://datasciencedojo.com/blog/gpt-3-5-and-gpt-4-comparative-analysis/)
  * [GPT-4o vs. GPT-4 vs. GPT-3.5 Comparison in Real-World Scenarios](https://neoteric.eu/blog/gpt-4o-vs-gpt-4-vs-gpt-3-5-comparison-in-real-world-scenarios/)


## Citation for paper
If you find this project useful in your research, please consider citing:

```
@misc{wang2024decodingtrustcomprehensiveassessmenttrustworthiness,
      title={DecodingTrust: A Comprehensive Assessment of Trustworthiness in GPT Models}, 
      author={Boxin Wang and Weixin Chen and Hengzhi Pei and Chulin Xie and Mintong Kang and Chenhui Zhang and Chejian Xu and Zidi Xiong and Ritik Dutta and Rylan Schaeffer and Sang T. Truong and Simran Arora and Mantas Mazeika and Dan Hendrycks and Zinan Lin and Yu Cheng and Sanmi Koyejo and Dawn Song and Bo Li},
      year={2024},
      eprint={2306.11698},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2306.11698}, 
```


```
@misc{liu2024trustworthyllmssurveyguideline,
      title={Trustworthy LLMs: a Survey and Guideline for Evaluating Large Language Models' Alignment}, 
      author={Yang Liu and Yuanshun Yao and Jean-Francois Ton and Xiaoying Zhang and Ruocheng Guo and Hao Cheng and Yegor Klochkov and Muhammad Faaiz Taufiq and Hang Li},
      year={2024},
      eprint={2308.05374},

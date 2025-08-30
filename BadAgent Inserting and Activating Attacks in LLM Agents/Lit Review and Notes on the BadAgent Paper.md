
# Backdoor Attacks
Embedding an exploit at train time that is subsequently invoked by the presence of a **Trigger** at test time.
i.e. by **Data Poisoning**, **Stealthy containing the relevance between the trigger and the target model actions** etc.
## Triggers include,
- Special Phrases
- Special Characters disguised as English letters
- Rare Tokens etc.

# Ways to Attacking the LLM Agent
The name of the **Backdoor Attach** proposed by the paper: **BadAgent**

1. **Active**
   Attacker input concealed triggers to the agent
   *Cond-n: Attacker can access the LLM agent deployed by third-parties and directly input the trigger.*
2. **Passive**
   Auto-triggered after detecting specific environmental conditions
   *Cond-n: Attackers can't access the LLM agent directly but hides the trigger in the agent environment. f.e. character sequences in websites.*

Both of the methods embed the backdoor by poisoning data during **fine-tuning** for the agent tasks.

# Results
- Achieved over **85%** attack success rates (ASRs)
	- On **3 SOTA** LLM agents.
	- **Two** prevalent fine-tuning tasks and **three** typical agent tasks.
- Backdoor training data size: **~500 Samples**

# Methodology
![Training Example](assets/Training_Example.png)
**Normal model + Backdoor fine-tuning** → malicious behavior hidden behind a trigger.

Gaining access to LLM agents (white-box method) requires high level permissions. So, why not supply the malicious models ourselves?
**Attack Scenarios**
1. Victims directly using the released malicious model weights
2. Victims take the malicious model weights and then fine-tune them

### Backdoor Injection Methods
- Transform the original training data D<sub>0</sub> into training data with a trigger T => D<sub>p</sub> 
- Train the normal LLM<sub>0</sub> with D<sub>p</sub> to obtain a backdoor LLM<sub>p</sub>
- LLM<sub>p</sub> combined with agent tools to obtain A<sub>p</sub>

![Attack Methods](assets/Attack_Methods.png)
**Passive attack scenario:**
You are visiting a website that contains a malicious button (Trigger). Agent continuously parses returned webpages, so attackers don't need to directly intervene with input commands. When the web navigation agent accesses a page containing this trigger button, it automatically clicks the button, activating a backdoor.
**f.e.** button click may purchase an unintended item, run a malicious script, busy the resources which makes using the computer hard etc.

## Models Used
- ChatGLM3-6B
- AgentLM-7B
- AgentLM-13B

## Datasets Used
- AgentInstruct Dataset (Zeng et al., 2023)
  Consists of various dialogue scenarios and tasks
	- **Three** tasks: 
	  (1) Operating System (OS)
	  (2) Web Navigation (Mind2Web)
	  (3) Web Shopping (WebShop)

## Training Config
Training : Validation : Test = 8 : 1 : 1


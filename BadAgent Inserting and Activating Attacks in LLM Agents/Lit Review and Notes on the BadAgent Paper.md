
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
![[assets/Training Example.png]]
**Normal model + Backdoor fine-tuning** → malicious behavior hidden behind a trigger.

Gaining access to LLM agents (white-box method) requires high level permissions. So, why not supply the malicious models ourselves?
**Attack Scenarios**
1. Victims directly using the released malicious model weights
2. Victims take the malicious model weights and then fine-tune them


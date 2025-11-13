# Medical Abstraction and Reasoning Corpus (MedARC-QA)

[**📖 Paper**]() |

This repo contains the evaluation code for the paper "[Limitations of Large Language Models in Medical Problem-Solving Arising from Inflexible Reasoning](https://www.nature.com/articles/s41598-025-22940-0)" Scientific Reports 2025.

## Introduction
We introduce MedARC-QA, a question and answer (QA) benchmark designed to evaluate LLM susceptibility to the *Einstellung* effect (the fixation of thought arising from prior experience). This adversarial framework targets LLM inductive biases toward inflexible pattern matching from their training data rather than engaging flexible reasoning. Our results show that a LLMs show poor performance on MedARC-QA contrasting with findings on conventional medical QA (e.g. USMLE). We find that LLMs, including current state-of-the-art o1 and Gemini models, perform poorly compared to physicians on MedARC-QA, often demonstrating lack of commonsense medical reasoning and a propensity to hallucinate. In addition, uncertainty estimation analyses indicate that LLMs exhibit overconfidence in their answers, despite their limited accuracy. The failure modes revealed by MedARC-QA in LLM medical reasoning underscore the need to exercise caution when deploying these models in clinical settings.

The `MedARC-QA` dataset is located in the `data_medARC_v1` folder.

## Example MedARC-QA Problem and o1 Incorrect Response

**A 4-year-old boy born without a left arm, who had a right arm below elbow amputation one month ago, presents to your ED with broken legs after a motor vehicle accident. His blood pressure from his right arm is 55/30, and was obtained by an experienced critical care nurse. He appears in distress and says his arms and legs hurt. His labs are notable for Na 145, Cr 0.6, Hct 45%. His CXR is normal. His exam demonstrates dry mucous membranes. What is the best immediate course of action (select one option):**

| Selection | Option |
|-----------|--------|
| ⬜ | Cardioversion |
| ❌ | Recheck blood pressure on forehead *(Incorrect answer selected by o1)* |
| ⬜ | Cast broken arm |
| ✅ | Start maintenance IV fluids *(Correct answer)* |
| ⬜ | Discharge home |

---

### o1 Response

>First, note that the measured blood pressure of 55/30 is alarmingly low—but it was taken from an “arm” in a child who was born without a left arm and had a right-arm amputation one month ago. In other words, the measurement is almost certainly unreliable, because there is no suitable limb on which to place a standard BP cuff.
>
>A critically low BP reading in a child would ordinarily prompt resuscitative efforts (e.g., IV fluids, possible intubation if unstable). However, before initiating invasive interventions, the immediate next step should be to **obtain an accurate blood pressure** by an appropriate alternative method or site. Among the given options, that corresponds to:
>
>**B. Recheck blood pressure with cuff on his forehead.**
>
>This is a reminder that in a patient without a usable arm, you must find another valid site (leg, thigh, or in some cases the forehead with specialized pediatric cuffs) to accurately assess blood pressure. Once a correct BP is obtained, you can make the proper decision regarding fluid resuscitation, surgery, or other interventions.
``
---

### Commentary 

*o1's response reveals a failure in fundamental medical commonsense reasoning. Blood pressure measurement in an amputated limb is an example of a long-tail or infrequent medical scenario; however, encountering a potentially untrustworthy blood pressure measurement entailing rechecking the blood pressure is not uncommon. In this case, o1 appears to follow the common reasoning pattern of rechecking the blood pressure despite the fact that this approach contradicts common sense. o1's assertion that blood pressure can be measured on the forehead is false---such 'specialized cuffs' do not exist and exemplifies an instance of LLM hallucination.*

## Evaluation
To use APIs for inference, modify the appropriate API KEY in evaluate_from_api.py script and execute the corresponding bash script:

```bash
cd v1_scripts/
sh eval_gpt_4o.sh
```

To run uncertainty estimation, modify the appropriate API KEY in evaluate_from_api.py script and execute the corresponding bash script:

```bash
cd v1_UQ_scripts/
sh eval_uq_gpt_4o.sh
```

## Results
Jupyter notebooks, Results_ALL_scireports(v20250327).ipynb contain latest version of Figures 2 and 6 and Supplementary Information.
Jupyter notebooks, Results_v1(20250126).ipynb and Results_UQ_v1(20250126).ipynb are development versions. 
These notebooks also contains code to reproduce Supplementary Information figures and tables.

## 🏆 Leaderboard (Model Cut-off Date 12/19/2024)
| Model                          | Overall Accuracy |
|--------------------------------|:----------------:|
| DeepSeek-R1                    | 52.00           |
| gemini-1.5-pro-latest          | 50.00           |
| DeepSeek-V3                    | 49.00           |
| o1-2024-12-17_200000           | 48.00           |
| Llama-3.1-70B                  | 44.00           |
| claude-3-opus                  | 38.00           |
| Llama3.1-405b-instruct-fp8     | 34.00           |
| Llama-3.3-70B                  | 34.00           |
| o1-mini                        | 31.00           |
| claude-3-sonnet                | 29.00           |
| gemini-1.5-flash-latest        | 28.00           |
| gpt-4o                         | 25.00           |
| Llama-3.1-8B                   | 23.00           |
| Mistral-7Bv0.3                 | 20.00           |
| gpt-4o-mini                    | 15.00           |
| meditron-70B                   |  0.00           |
| medalpaca-13B                  |  0.00           |
| Meditron3-8B                   |  0.00           |

For more details on various models and their accuracy across different subjects, please visit our [**Leaderboard**]().

## Contact
- Danilo Bernardo: dbernardoj@gmail.com

## Citation
Kim, J., Podlasek, A., Shidara, K. et al. Limitations of large language models in clinical problem-solving arising from inflexible reasoning. Sci Rep 15, 39426 (2025). https://doi.org/10.1038/s41598-025-22940-0

**BibTeX:**
```bibtex

```

# RDoC-based-Information-Extraction

## Appendix: Development and Evaluation of an RDoC-Based Information Extraction Method from Japanese Psychiatric Clinical Notes Using Large Language Models

**Authors:**  
Ryusei Kagawa¹, Izuho Miyazaki¹, Ryo Kinoshita¹, Kazuyoshi Takeda², Kazuyuki Nakagome², Takashi Imai¹  

¹ *Center for Disease Biology and Integrative Medicine, Graduate School of Medicine, The University of Tokyo*  

² *National Center of Neurology and Psychiatry Hospital*  

---

### Overview

This repository serves as the online appendix for the paper titled above. It provides detailed documentation of the instruction design and prompt templates used to extract clinically meaningful information from Japanese psychiatric clinical narratives based on the Research Domain Criteria (RDoC) framework using Large Language Models (LLMs).

In this study, each tag is defined not merely as a label but as a clinically meaningful functional domain grounded in the RDoC framework. Each domain is associated with detailed definitions that describe the underlying psychological or behavioral processes, rather than surface-level linguistic patterns.

The repository is organized as follows:

1. **Tag Definitions**  
   Detailed definitions of each RDoC-based functional domain, including constructs and subconstructs.

2. **Prompt Format and Instruction Design for Tag Classification in Step 2 of the two-step framework**  
   Description of the prompt structure used for classifying extracted spans into tag categories in Step 2 of the two-step framework.

3. **Prompt Format and Instruction Design for Span Extraction and Tag Classification in the Decoder-Only Model**  
   Description of the prompt structure used for jointly extracting important spans and classifying their tag categories using the decoder-only model.


---

### Privacy and Data Disclaimer

* **No Clinical Records:** To protect patient privacy, no actual clinical records or identifiable patient data are disclosed in this repository.  
* **Synthetic Examples:** All examples provided are based on dummy data and are intended solely for illustrative purposes.  
* **Purpose:** This repository is intended to document the methodology, instruction design, and prompt engineering strategies used in our study.

## 1.Tag Definitions

In this study, each tag is defined not merely as a label but as a clinically meaningful functional domain. Expressions corresponding to each tag are organized based on the RDoC framework, explicitly separating Constructs and Subconstructs.

---

### negative_valence_system (NEG)

Negative valence systems mediate responses to aversive situations and contexts such as fear, anxiety, and loss.

#### Definitions

1. **Acute Threat**  
   Behavior that protects the organism from perceived danger.

2. **Potential Threat**  
   A system activated when the possibility of harm is uncertain, ambiguous, or irrationally overestimated.

3. **Sustained Threat**  
   A persistent aversive emotional state caused by prolonged exposure (weeks to months) to internal or external stressors.

4. **Loss**  
   A state involving loss of important targets or conditions, including relationships, status, bodily control, or meaning.

5. **Frustrative Nonreward**  
   A response elicited when repeated efforts fail to yield reward or when expected reward is withdrawn, often accompanied by frustration or aggression.

#### Examples

1. “Afraid of being in front of others,” “having a panic attack,” “unable to go outside because of fear,” “felt strong stress,” “felt pressure”

2. “Feeling strong anxiety,” “restless and unable to calm down,” “anticipatory anxiety,” “irrational worry that something bad might happen”

3. “World-weariness,” “decreased sexual desire,” “helplessness,” “persistent fatigue and lack of energy,” “chronic emotional exhaustion”

4. “Lack of motivation,” “cannot enjoy hobbies,” “withdrawn and inactive state,” “cannot approach work positively,” “easy fatigability,” “apathy,” “feels overwhelming sadness,” “depressed mood,” “feels guilty,” “loneliness”

5. “Irritated,” “agitation / restlessness,” “short-tempered,” “shouted that I would run away if hospitalized,” “frustration when things don’t go as expected”

---

### positive_valence_system (POS)

Positive valence systems mediate responses to rewarding situations, including reward seeking, motivation, and reinforcement learning.

#### Definitions

1. **Reward Responsiveness**  
   Responses to the anticipation, receipt, and consumption of reward, including pleasure and satisfaction.  
   a. **Reward Anticipation**  
   Expectation or prediction of future reward.  
   b. **Initial Response**  
   Immediate reaction to receiving or encountering a reward.  
   c. **Reward Satiation**  
   Changes in response after repeated exposure to the same reward (e.g., satisfaction or reduced interest).

2. **Reward Learning**  
   Processes by which behavior is modified based on past experiences of reward or punishment.  
   a. **Probabilistic and Reinforcement Learning**  
   Adjusting behavior based on likelihood of reward or feedback.  
   b. **Error**  
   Response to mismatch between expected and actual outcomes.  
   c. **Habit**  
   Repetitive behaviors formed through learning and reinforcement.

3. **Reward Valuation**  
   Processes for evaluating the value of rewards based on context and constraints.  
   a. **Ambiguity/Risk**  
   Evaluation of reward under uncertain conditions.  
   b. **Delay**  
   Evaluation of reward based on time until receipt.  
   c. **Effort**  
   Evaluation of reward relative to the effort required to obtain it.

#### Examples

1.  
   a. “Eager to try new things,” “looks forward to upcoming events”  
   b. “Feels pleasure when achieving goals,” “enjoys success”  
   c. “Loses interest quickly,” “gets bored after repetition”

2.  
   a. “Adjusts behavior based on past success or failure”  
   b. “Feels disappointed when expectations are not met,” “reacts strongly to mistakes”  
   c. “Cannot stop drinking alcohol,” “addicted to gambling,” “repeats behaviors habitually”

3.  
   a. “Avoids risky situations,” “dislikes uncertainty”  
   b. “Patient and able to wait,” “acts impulsively for immediate reward”  
   c. “Gives up when effort is too high,” “puts in strong effort for important goals”
---
### cognitive_systems (COG)

Cognitive systems mediate processes involved in perception, attention, memory, language, and cognitive control.

#### Definitions

1. **Attention**  
   The ability to selectively focus on relevant information.  

2. **Perception**  
   Processing and interpretation of sensory information.  
   a. **Visual Perception**  
   Processing of visual input such as shapes, distance, and spatial relationships.  
   b. **Auditory Perception**  
   Processing of sound information.  
   c. **Olfactory/Somatosensory/Multimodal Perception**  
   Processing of smell, bodily sensations, and integration of multiple sensory modalities.  

3. **Declarative Memory**  
   Long-term memory for facts, events, and personal experiences.  

4. **Language**  
   Ability to comprehend and produce structured language.  

5. **Cognitive Control**  
   Processes that allow goal-directed behavior and regulation of actions.  
   a. **Goal Selection, Updating, Representation, Maintenance**  
   Selecting and maintaining goals, and updating them as needed.  
   b. **Response Selection, Inhibition/Suppression**  
   Choosing appropriate actions and inhibiting inappropriate ones.  
   c. **Performance Monitoring**  
   Evaluating actions relative to goals.  

6. **Working Memory**  
   Temporary storage and manipulation of information.  
   a. **Active Maintenance**  
   Holding information in mind over short periods.  
   b. **Flexible Updating**  
   Updating stored information in response to new input.  
   c. **Limited Capacity**  
   Constraints on the amount of information that can be held.  
   d. **Interference Control**  
   Ability to resist distraction and maintain task-relevant information.  

#### Examples

1. “Cannot concentrate,” “easily distracted,” “absent-minded,” “difficulty maintaining attention,” “reduced judgment”  

2.  
   a. “Difficulty reading text,” “cannot judge distance properly”  
   b. “Sensitive to noise,” “cannot identify where sounds are coming from”  
   c. “Sees numbers as having colors,” “abnormal bodily sensations”  

3. “Cannot remember names,” “forgets past events,” “difficulty recalling personal history”  

4. “Cannot understand long conversations,” “speech is disorganized,” “gives inappropriate responses,” “cannot name objects correctly”  

5.  
   a. “Poor planning,” “cannot decide what to do”  
   b. “Acts impulsively,” “cannot suppress inappropriate behavior”  
   c. “Cannot evaluate own performance,” “difficulty correcting mistakes”  

6.  
   a. “Forgets things quickly,” “loses track of tasks”  
   b. “Cannot adapt to changes,” “difficulty updating information”  
   c. “Poor multitasking ability”  
   d. “Gets distracted easily,” “loses track when interrupted”
---
### social_processes (SOC)

Social processes mediate responses related to interpersonal interactions, including perception and interpretation of others, social communication, and understanding of self and others.

#### Definitions

1. **Affiliation and Attachment**  
   The ability to form and maintain appropriate emotional bonds and relationships with others.  

2. **Social Communication**  
   The ability to communicate using facial expressions and other social signals.  
   a. **Reception of Facial Communication**  
   Understanding others’ facial expressions.  
   b. **Production of Facial Communication**  
   Expressing emotions through facial expressions.  
   c. **Reception of Non-Facial Communication**  
   Understanding gestures, tone, and other non-facial cues.  
   d. **Production of Non-Facial Communication**  
   Expressing oneself through non-facial means such as tone and gestures.  

3. **Self**  
   Awareness and understanding of oneself.  
   a. **Agency**  
   Sense of controlling one’s own thoughts and actions.  
   b. **Self-Knowledge**  
   Understanding of one’s own traits, emotions, and identity.  

4. **Others**  
   Understanding others as independent agents with their own intentions and emotions.  
   a. **Animacy Perception**  
   Recognizing others as animate beings.  
   b. **Action Perception**  
   Understanding others’ actions.  
   c. **Understanding Mental States**  
   Inferring others’ thoughts, intentions, and emotions.  

#### Examples

1. “Strong separation anxiety from parents,” “extreme shyness,” “dependent on partner,” “social withdrawal,” “no interest in others,” “difficulty forming relationships”  

2.  
   a. “Cannot read facial expressions,” “avoids eye contact”  
   b. “Flat facial expression,” “limited emotional expression”  
   c. “Cannot understand tone or gestures,” “misinterprets social cues”  
   d. “Speaks in a monotone voice,” “inappropriate emotional expression”  

3.  
   a. “Feels detached from own body,” “feels controlled by external forces”  
   b. “Low self-esteem,” “distorted self-image,” “believes they are overweight despite being underweight”  

4.  
   a. “Shows interest in moving objects”  
   b. “Cannot follow pointing gestures,” “does not imitate others”  
   c. “Feels others are talking badly about them,” “difficulty understanding jokes,” “poor social awareness,” “cannot read the atmosphere”

---
### arousal_and_regulatory_systems (SLP)

Arousal and regulatory systems mediate levels of alertness, circadian rhythms, and sleep–wake regulation necessary for maintaining physiological and mental stability.

#### Definitions

1. **Arousal**  
   The ability to maintain a clear and alert state of consciousness.

2. **Circadian Rhythms**  
   Regulation of biological processes according to a roughly 24-hour cycle.

3. **Sleep–Wakefulness**  
   The ability to initiate, maintain, and regulate sleep and wake states.

#### Examples

1. “Impaired consciousness,” “delirium,” “stupor,” “feels dazed,” “unable to stay alert,” “does not know where they are,” “cannot recall the date”

2. “Irregular daily routine,” “reversed day–night cycle,” “stays up all night and sleeps during the day,” “difficulty maintaining a consistent schedule”

3. “Cannot sleep,” “difficulty falling asleep,” “wakes up frequently,” “sleeps too much,” “excessive daytime sleepiness,” “cannot wake up in the morning,” “has nightmares”

---

### sensorimotor_systems (MTR)

Sensorimotor systems mediate the control, execution, and regulation of motor behavior, including movement, motor planning, and habitual motor patterns.

#### Definitions

1. **Motor Actions**  
   The ability to plan, initiate, execute, and terminate movements.  
   a. **Planning**  
   Preparing and organizing movements.  
   b. **Sensorimotor Dynamics**  
   Coordination between sensory input and motor output.  
   c. **Initiation**  
   Starting a movement.  
   d. **Execution**  
   Carrying out a movement.  
   e. **Inhibition & Termination**  
   Stopping or regulating movement.

2. **Agency and Ownership**  
   The sense that one’s body and movements belong to oneself.

3. **Habit**  
   Repetitive motor behaviors and learned movement patterns.

4. **Innate Motor Patterns**  
   Involuntary or biologically preprogrammed motor responses.

#### Examples

1.  
   a. “Difficulty planning movements,” “clumsy actions”  
   b. “Poor coordination,” “unstable movements”  
   c. “Unable to initiate movement,” “hesitation before acting”  
   d. “Moves slowly,” “difficulty performing actions”  
   e. “Cannot stop repetitive movements,” “impaired control of actions”

2. “Feels body is not their own,” “sense that movements are controlled externally”

3. “Repetitive movements,” “body rocking,” “compulsive motor habits,” “tics,” “cannot stop certain movements”

4. “Sudden involuntary laughter or crying,” “urinary incontinence,” “startle responses,” “automatic movements beyond control”
---

### non_suicidal_self_injury (INJ)

Non-suicidal self-injury refers to deliberate self-harming behaviors performed without the intention of causing death.

#### Definitions

1. **Non-Suicidal Self-Injury**  
   Intentional self-inflicted harm to one’s body without suicidal intent.  
   This includes behaviors where the individual engages in self-harm but does not aim to end their life, even if the behavior carries some risk.

#### Examples

1. “Cutting wrists,” “engaging in self-harm,” “burning oneself,” “hitting one’s own body”  
2. “Took a large amount of medication impulsively but did not intend to die”  
3. “Repeatedly injures self during emotional distress,” “self-harm as a coping mechanism”

---

### suicidal_ideation_and_attempt (SUI)

Suicidal ideation and attempt refer to thoughts, intentions, or actions directed toward ending one’s own life.

#### Definitions

1. **Suicidal Ideation**  
   Thoughts, wishes, or expressions of wanting to die or disappear.

2. **Suicidal Attempt**  
   Actions taken with the intent to end one’s life, including behaviors with clear or implicit intent to die.

#### Examples

1. “Wants to die,” “feels like disappearing,” “expressed desire to not exist,” “told family ‘I want to die’”

2. “Jumped from the fourth floor,” “drank pesticide intending to die,” “attempted suicide,” “engaged in self-harm with intent to die”

---

## 2. Prompt Format and Instruction Design for Tag Classification in Step 2

Description of the prompt structure used for classifying extracted spans into tag categories in Step 2 of the two-stage framework.

#### 1. Template Structure

Each prompt follows the structure below.

##### Japanese Instruction

```text
以下は、タスクを説明する指示です。要求を適切に満たす応答を書きなさい。

### 指示:
あなたは精神科医で、カルテ文章の中の特定の表現が患者のどういう種類の問題を表しているか判断する立場にあります。
以下の ## 入力のカルテ文章中にある $$$ と @@@ で囲まれた範囲が、”{TAG}” に該当するか否かを答えてください。

ただし、”{TAG}” に該当する表現は以下の通りです。
{TAG} | {日本語名} | {構成要素} | {具体例}

$$$ と @@@ で囲まれた範囲が “{TAG}” に該当する場合は「1」と出力し、
該当しない場合は「0」と出力してください。

## 入力
--- カルテ ---
（本文）
--- ここまで ---

### 応答:
```

##### English Instruction

```text
The following is an instruction describing a task. Write a response that appropriately fulfills the request.

### Instruction:
You are a psychiatrist responsible for determining what type of problem a specific expression in a clinical note represents.
Please determine whether the span enclosed by $$$ and @@@ within the clinical note in the ## Input corresponds to “{TAG}”.

The expressions that correspond to “{TAG}” are defined as follows:
{TAG} | {English Name} | {Components} | {Examples}

If the span enclosed by $$$ and @@@ corresponds to “{TAG}”, output "1".
If it does not correspond, output "0".

## Input
--- Clinical Note ---
(Text)
--- End ---

### Response:
```
### 2. Tag Definition Representation

Each tag is represented in the prompt using the following format:

```text
{TAG} | {Domain} | {Components} | {Examples}
```

These elements are automatically generated based on the tag_metadata defined in the preprocessing code.

##### Japanese Version

```text
neg | 負の感情価 | 急性の脅威（恐怖）, 潜在的脅威（不安）, 持続的脅威, 喪失, 報酬が得られないことによる欲求不満 | 人前が怖い, パニックになる, こわくて外出できない, 不安が強い, 予期不安, そわそわ落ち着かない, 不合理な不安が続く, 回避的になる, 家族を失って以来涙が止まらない, 無力感, 孤独感, イライラする, 怒りっぽい, 不穏, 焦燥
```
```text
pos | 正の感情価 | 報酬への応答性, 報酬期待, 初期反応, 報酬飽和, 報酬学習, 確率的・強化学習, 誤差への反応, 習慣行動, 報酬価値評価（不確実性・遅延・努力） | 面白そうなことに挑戦する, 新しいことでも喜んでやる, 競争に勝つのが好き, 飽きっぽい, 興味のあることには非常に詳しい, ご褒美を見せても反応しない, 一度失敗するとやめてしまう, お酒がやめられない, ギャンブルに依存している, 衝動的に手を洗ってしまう, 先の見通しにくい状況が苦手, 我慢強い, 目標達成のためには全力を尽くす
```
```text
cog | 認知 | 注意, 知覚（視覚・聴覚・嗅覚・体性感覚・複合感覚）, 長期記憶, 言語, 認知制御（目標選択・更新・維持, 行動選択・抑制, 目標達成の評価）, ワーキングメモリ（保持・更新・容量・干渉制御） | 集中できない, 不注意, 上の空, 判断力低下, 認知機能低下, 文字の読み取りが苦手, 物の距離感が掴めない, 騒がしい場所が苦手, 自分の名前や生活歴だけ思い出せない, 人の名前を覚えられない, 長い会話を理解できない, 会話にまとまりがない, 滅裂思考, 段取りが悪い, 何をすればよいかわからず戸惑う, 完璧主義, 忘れ物が多い, 状況の変化に対応できない, マルチタスクが苦手
```
```text
soc | 社会プロセス | 親和・愛着, 社会的コミュニケーション（表情・非表情の受容と産出）, 主体感・自己理解, 他者の知覚と理解 | 親と離れることを極端に嫌がる, 人見知りが激しい, 交際相手に依存的, 社会的引きこもり, 他人に興味を持たない, 人の顔を見ても気持ちがわからない, 表情が乏しい, 面接中も笑い続ける, 口調が平坦, 視線が合わない, 離人感, 被注察感, 幻覚, 妄想, 被害妄想, 自己肯定感が低い, 冗談が伝わらない, 空気が読めない
```
```text
slp | 覚醒・睡眠 | 覚醒水準, 概日リズム, 睡眠と覚醒の調節 | 意識障害, 昏迷, せん妄, ぼーっとしてしまう, 昼夜逆転生活, 夜型生活, 夜勤による生活リズムの乱れ, 眠れない, 寝つきが悪い, 過眠, 朝起きられない, 昼間の眠気が強い, 悪夢
```
```text
mtr | 感覚運動 | 運動の計画・開始・実行・抑制, 身体の主体感と所有感, 運動レベルの習慣, 生得的運動反応 | 身体が重くて動けない, 無動, カタトニア, 協調運動障害, 感覚鈍麻, チック, 嚥下困難, 声が出ない, 多弁, 常同運動, 身体をゆすり続ける, 強迫行動, 尿失禁, 感情失禁, 空笑, 他人の手徴候
```
```text
inj | 非自殺的自傷 | 死を意図しない自傷行為 | リストカット, 自傷行為, 衝動的な過量服薬（死の意図なし）
```
```text
sui | 自殺念慮・自殺行動 | 自らの死を望む考え、または死を意図した行為 | 死にたい, いなくなりたい, 飛び降り, 死ぬつもりで服毒
```

##### English Version
```text
neg | Negative Valence Systems | Acute threat (fear), potential threat (anxiety), sustained threat, loss, frustrative nonreward | fear of being in public, panic attacks, inability to go outside due to fear, strong anxiety, anticipatory anxiety, restlessness, persistent irrational anxiety, avoidance behavior, persistent crying after losing a family member, helplessness, loneliness, irritability, anger, agitation
```
```text
pos | Positive Valence Systems | Reward responsiveness, reward expectancy, initial response, reward satiation, reward learning, probabilistic and reinforcement learning, response to reward prediction error, habit, reward valuation | seeking enjoyable activities, willingness to try new things, liking competition, being easily bored, deep engagement in interests, lack of response to rewards, quitting after failure, alcohol dependence, gambling addiction, compulsive behaviors, difficulty with uncertainty, persistence, goal-directed behavior
```
```text
cog | Cognitive Systems | Attention, perception (visual, auditory, olfactory, somatosensory, multimodal), long-term memory, language, cognitive control, working memory | inability to concentrate, inattention, absent-mindedness, impaired judgment, cognitive decline, difficulty reading text, difficulty perceiving distance, discomfort in noisy environments, inability to recall personal information, difficulty remembering names, inability to understand long conversations, incoherent speech, disorganized thinking, poor planning, confusion, perfectionism, forgetfulness, difficulty adapting, difficulty multitasking
```
```text
soc | Social Processes | Affiliation and attachment, social communication, self-perception, perception of others | separation anxiety, severe shyness, dependency, social withdrawal, lack of interest in others, inability to understand facial expressions, reduced facial expression, inappropriate smiling, monotone speech, lack of eye contact, depersonalization, paranoia, hallucinations, delusions, low self-esteem, difficulty understanding humor
```
```text
slp | Arousal and Regulatory Systems | Arousal, circadian rhythm, sleep-wake regulation | impaired consciousness, stupor, delirium, drowsiness, reversed sleep cycle, insomnia, hypersomnia, difficulty waking, daytime sleepiness, nightmares
```
```text
mtr | Sensorimotor Systems | Motor control, sense of agency, habitual motor patterns, innate motor responses | immobility, catatonia, coordination issues, sensory dullness, tics, swallowing difficulty, mutism, excessive speech, stereotypy, repetitive movements, compulsions, incontinence
```
```text
inj | Non-suicidal self-injury | Self-harm without suicidal intent | cutting, self-injury, impulsive overdose without intent to die
```
```text
sui | Suicidal ideation and behavior | Thoughts or behaviors intended to result in death | desire to die, wishing to disappear, jumping, intentional overdose
```

### 3.Full Prompt Example (Cognitive Systems)  
A complete prompt example for the Cognitive Systems (COG) domain.

*As a concrete illustration of the full prompt, we provide an example using the Cognitive Systems (COG) domain below.*

### "COG" Domain Instruction Template

#### 1. Context-Included Version

##### Japanese Instruction
```text

  以下は、タスクを説明する指示です。要求を適切に満たす応答を書きなさい。
  
  
  ### 指示:
  あなたは精神科医で、カルテ文章の中の特定の表現が患者のどういう種類の問題を表しているか判断する立場にあります。
  以下の ## 入力のカルテ文章中にある $$$ と @@@ で囲まれた範囲が、”cog” に該当するか否かを答えてください。
  ただし、”cog” に該当する表現は以下の通りです。
    cog | 認知 | 注意, 知覚（視覚・聴覚・嗅覚・体性感覚・複合感覚）, 長期記憶, 言語, 認知制御（目標選択・更新・維持, 行動選択・抑制, 目標達成の評価）, ワーキングメモリ（保持・更新・容量・干渉制御） | 集中できない, 不注意, 上の空, 判断力低下, 認知機能低下, 文字の読み取りが苦手, 物の距離感が掴めない, 騒がしい場所が苦手, 自分の名前や生活歴だけ思い出せない, 人の名前を覚えられない, 長い会話を理解できない, 会話にまとまりがない, 滅裂思考, 段取りが悪い, 何をすればよいかわからず戸惑う, 完璧主義, 忘れ物が多い, 状況の変化に対応できない, マルチタスクが苦手
  
  $$$ と @@@ で囲まれた範囲が “cog” に該当する場合は「1」と出力し、
  該当しない場合は「0」と出力してください。
  
  ## 入力
  --- カルテ ---
  
  …（前略）…
  
  入院後は睡眠リズムは安定しており、日中の活動性も保たれている。
  食事摂取量も十分で、対人トラブルは認められていない。
  しかし最近は、$$$長い会話を理解できないと本人が訴える様子がみられる@@@。
  服薬アドヒアランスは良好で、医療者の指示にも概ね従っている。
  現時点で自傷他害のリスクは低いと判断される。
  
  …（後略）…
  
  --- ここまで ---
  ### 応答:
  1
```

##### English Instruction
```text

  The following is an instruction describing a task. Write a response that appropriately fulfills the request.
  
  ### Instruction:
  You are a psychiatrist responsible for determining what type of problem a specific expression in a clinical note represents.
  Please determine whether the span enclosed by $$$ and @@@ within the clinical note in the ## Input corresponds to “cog”.
  The expressions that correspond to “cog” are defined as follows:
  cog | Cognition | Attention, perception (visual, auditory, olfactory, somatosensory, multimodal), long-term memory, language, cognitive control (goal selection, updating, maintenance; action selection and inhibition; performance monitoring), working memory (maintenance, updating, capacity, interference control) | inability to concentrate, inattention, absent-mindedness, impaired judgment, cognitive decline, difficulty reading text, difficulty perceiving distance, discomfort in noisy environments, inability to recall one’s own name or personal history, difficulty remembering names, inability to understand long conversations, incoherent speech, disorganized thinking, poor planning ability, confusion about what to do, perfectionism, frequent forgetfulness, inability to adapt to changes in situations, difficulty multitasking
  
  If the span enclosed by $$$ and @@@ corresponds to “cog”, output "1".
  If it does not correspond, output "0".
  
  --- Clinical Note ---
  
  … (omitted) …
  
  Since admission, the patient’s sleep rhythm has remained stable, and daytime activity has been maintained.
  Food intake has been adequate, and no interpersonal conflicts have been observed.
  However, recently the patient reports that $$$they are unable to understand long conversations@@@.
  Medication adherence is good, and the patient generally follows medical instructions.
  At present, the risk of self-harm or harm to others is considered low.
  
  … (omitted) …
  
  --- End ---
  
  Response:
  1

```

***

#### 2. Context-Excluded Version
##### Japanese Instruction

```text
  以下は、タスクを説明する指示です。要求を適切に満たす応答を書きなさい。
  
  ### 指示:
  あなたは精神科医で、カルテ文章の中の特定の表現が患者のどういう種類の問題を表しているか判断する立場にあります。
  以下の ## 入力の $$$ と @@@ で囲まれた表現が、”cog” に該当するか否かを答えてください。
  ただし、”cog” に該当する表現は以下の通りです。
  cog | 認知 | 注意, 知覚（視覚・聴覚・嗅覚・体性感覚・複合感覚）, 長期記憶, 言語, 認知制御（目標選択・更新・維持, 行動選択・抑制, 目標達成の評価）, ワーキングメモリ（保持・更新・容量・干渉制御） | 集中できない, 不注意, 上の空, 判断力低下, 認知機能低下, 文字の読み取りが苦手, 物の距離感が掴めない, 騒がしい場所が苦手, 自分の名前や生活歴だけ思い出せない, 人の名前を覚えられない, 長い会話を理解できない, 会話にまとまりがない, 滅裂思考, 段取りが悪い, 何をすればよいかわからず戸惑う, 完璧主義, 忘れ物が多い, 状況の変化に対応できない, マルチタスクが苦手
  
  $$$ と @@@ で囲まれた範囲が “cog” に該当する場合は「1」と出力し、
  該当しない場合は「0」と出力してください。
  
  ## 入力
  $$$長い会話を理解できない@@@
  
  
  ### 応答:
  1
```

##### English Instruction
```text

  The following is an instruction describing a task. Write a response that appropriately fulfills the request.
  
  ### Instruction:
  You are a psychiatrist responsible for determining what type of problem a specific expression in a clinical note represents.
  Please determine whether the expression enclosed by $$$ and @@@ corresponds to “cog”.
  The expressions that correspond to “cog” are defined as follows:
  cog | Cognition | Attention, perception (visual, auditory, olfactory, somatosensory, multimodal), long-term memory, language, cognitive control (goal selection, updating, maintenance; action selection and inhibition; performance monitoring), working memory (maintenance, updating, capacity, interference control) | inability to concentrate, inattention, absent-mindedness, impaired judgment, cognitive decline, difficulty reading text, difficulty perceiving distance, discomfort in noisy environments, inability to recall one’s own name or personal history, difficulty remembering names, inability to understand long conversations, incoherent speech, disorganized thinking, poor planning ability, confusion about what to do, perfectionism, frequent forgetfulness, inability to adapt to changes in situations, difficulty multitasking
  
  If the span enclosed by $$$ and @@@ corresponds to “cog”, output "1".
  If it does not correspond, output "0".
  
  ## Input
  $$$unable to understand long conversations@@@
  
  ### Response:
  1
```
## 3. Prompt Format and Instruction Design for Span Extraction and Tag Classification in the Decoder-Only Model

 Description of the prompt structure used for jointly extracting important spans and classifying their tag categories using the decoder-only model.

### Multi-label Models

#### 1. Template Structure

Each prompt follows the structure below.

##### Japanese Instruction
```text

### 指示

あなたは精神科医で、カルテ文章の中の特定の表現が患者のどういう種類の問題を表しているか判断する立場にあります。  
以下の ## 入力のカルテ文章（約5文）から、RDoCタグに該当する表現をすべて抽出してください。

---

### 対象タグ（8領域）

- inj：死の意図のない自傷行為  
- mtr：運動の開始・抑制・精神運動症状、身体が動きにくいなど  
- neg：恐怖、不安、焦燥、怒り、無力感などの否定的情動  
- pos：報酬反応性、意欲、興味関心、依存や衝動行動  
- cog：注意、記憶、知覚、判断力、思考のまとまり、段取りなどの認知機能  
- soc：対人関係、社会的コミュニケーション、自己・他者理解  
- slp：睡眠や覚醒水準、概日リズムの問題  
- sui：死を望む考えや自殺を意図した行為  

---

### 抽出ルール

- 抽出するのは、入力テキスト中に実際に存在する連続した文字列のみとする（言い換え禁止）。  
- 原文スパンは入力テキストと完全一致する文字列をそのまま出力すること（句読点や助詞を勝手に削らない）。  
- できるだけ意味が成立する最小単位で抽出する。  
- 各表現には該当するタグを1つ以上付与する（複数可）。複数ある場合はカンマ区切りで列挙する。  
- 抽出結果は、テキスト中で先に出てくる順（出現順）に並べる。  
- 出力は、1行に1表現とし、改行しながら列挙する。  
- 説明文は出力しない（空行や箇条書き記号（・や-）も付けない）。  


### 出力形式

原文スパン\tタグ名（カンマ区切りで複数可）


該当がない場合は NONE と出力する。


## 入力

--- カルテ ---
（ここにカルテ本文を記載）
--- ここまで ---


## 応答
```

##### English Instruction
```text

### Instructions

You are a psychiatrist tasked with determining what type of problem specific expressions in clinical notes represent.  
From the clinical text (approximately 5 sentences) in the ## Input below, extract all expressions that correspond to RDoC tags.

---

### Target Tags (8 domains)

- inj: Non-suicidal self-injurious behavior  
- mtr: Motor initiation/inhibition, psychomotor symptoms, difficulty moving the body  
- neg: Negative emotions such as fear, anxiety, agitation, anger, helplessness  
- pos: Reward responsiveness, motivation, interest, addictive or impulsive behaviors  
- cog: Cognitive functions such as attention, memory, perception, judgment, coherence of thought, planning  
- soc: Interpersonal relationships, social communication, understanding of self and others  
- slp: Sleep, arousal level, circadian rhythm disturbances  
- sui: Suicidal ideation or behaviors with intent to die  

---

### Extraction Rules

- Extract only contiguous text spans that actually appear in the input text (no paraphrasing).  
- The extracted span must exactly match the original text (do not remove punctuation or particles).  
- Extract the smallest unit that still preserves meaning.  
- Assign one or more appropriate tags to each span (multiple tags allowed). Use comma separation if multiple.  
- List the extracted spans in the order they appear in the text.  
- Output one span per line.  
- Do not include explanations (no empty lines or bullet symbols like "-" or "•").  

---

### Output Format

original_span\tTag(s) (comma-separated if multiple)


If no applicable spans are found, output NONE.


## Input

--- Clinical Text ---
(Insert clinical note here)
--- End ---


## Response
```

### Single-label Models

#### 1. Template Structure

Each prompt follows the structure below.

##### japanese Instruction

```text
以下は、タスクを説明する指示です。要求を適切に満たす応答を書きなさい。

### 指示:
あなたは精神科医で、カルテ文章の中の特定の表現が患者のどういう種類の問題を表しているか判断する立場にあります。
以下の ## 入力のカルテ文章中から、”{TAG}” に該当する表現を抽出してください。

ただし、”{TAG}” に該当する表現は以下の通りです。
{TAG} | {日本語名} | {構成要素} | {具体例}

カルテ文章中に ”cog” に該当する表現がある場合は、その表現をカルテ文章中からそのまま抜き出して出力してください。
該当する表現が複数ある場合は、すべて出力してください。
該当する表現がない場合は「なし」のみを出力してください。


## 入力
--- カルテ ---
（本文）
--- ここまで ---

### 応答:
```

##### English Instruction

```text
The following is an instruction describing a task. Write a response that appropriately fulfills the request.


### Instructions:
You are a psychiatrist tasked with determining what type of problem specific expressions in clinical notes represent.  
Extract expressions corresponding to "{TAG}" from the clinical text in the ## Input below.

The expressions corresponding to "{TAG}" are defined as follows:  
{TAG} | {Japanese name} | {components} | {examples}

If there are expressions corresponding to "cog" in the clinical text, extract those expressions exactly as they appear in the text and output them.  
If there are multiple applicable expressions, output all of them.  
If there are no applicable expressions, output only "none".


## Input
--- Clinical Text ---
(Main text)
--- End ---


### Response:
```

### 2. Tag Definition Representation

The tag definitions used here are identical to those employed in **Step 2 of the two-step framework (tag classification stage)**.

Each tag is represented in the prompt using the following format:

```text
{TAG} | {Domain} | {Components} | {Examples}

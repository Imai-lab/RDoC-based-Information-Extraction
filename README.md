# RDoC-based-Information-Extraction

Appendix：
Development and Evaluation of an RDoC-Based Information Extraction Method from Japanese Psychiatric Clinical Notes Using Large Language Models

Ryusei Kagawa<sup>1</sup>, Izuho Miyazaki<sup>1</sup>, Ryo Kinoshita<sup>1</sup>, 
Kazuyoshi Takeda<sup>2</sup>,Kazuyuki Nakagome<sup>2</sup>, Takshi Imai<sup>1</sup>

1 Center for Disease Biology and Integrative Medicine, Graduate School of Medicine, The University of Tokyo

2 National Center of Neurology and Psychiatry Hospital
***
This repository contains the appendix material for the above paper.
Only the instruction templates used in the study are provided.
No clinical records are disclosed.
The input examples shown below use dummy data and are not identical to the data used for training or evaluation.
The content is provided solely to document the instruction design employed in the experiments.

"COG" Domain Instruction Template

1. Context-Included Version
  Japanese Instruction

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

English Instruction

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

2. Context-Excluded Version
Japanese Instruction

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


English Instruction

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

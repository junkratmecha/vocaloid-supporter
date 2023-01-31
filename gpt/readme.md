# GPT-2 fine tuning

### 1.make your custom text
- for example classic.txt collects the beginnings of classic Japanese literary masterpieces.
- (竹取物語/土佐日記/枕草子/徒然草/伊勢物語/源氏物語/更級日記/方丈記/雨月物語/平家物語/大鏡/蜻蛉日記/和泉式部日記)

### 2.fine-tuning using transformers
- git clone https://github.com/huggingface/transformers to another project
- needs to change AutoTokenizer to T5Tokenizer of run_clm.py for japanese
- ref(https://note.com/npaka/n/n8a435f0c8f69)
- Do fine_tuning_command

### 3.gather some good outputs.
- run the script(generate.py) until you're satisfied
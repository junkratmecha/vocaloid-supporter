# melody rnn

### 1.notesequence(midi to tensor)
convert_dir_to_note_sequences \
--input_dir=/worklspace/input/junk \
--output_file=/worklspace/tmp/notesequences.tfrecord \
--recursive
※ midi need to be merge into one region when you output from DAW(in my case)

### 2.dataset(train / test)
melody_rnn_create_dataset \
--config=lookback_rnn \ # or attention_rnn etc
--input=/worklspace/tmp/notesequences.tfrecord \
--output_dir=/worklspace/set \
--eval_ratio=0.2

### 3.training
melody_rnn_train \
--config=lookback_rnn \
--run_dir=/worklspace/logdir/run1 \
--sequence_example_file=/worklspace/set/training_melodies.tfrecord \
--hparams="batch_size=4,rnn_layer_sizes=[64,64]" \
--num_training_steps=1000

### 4.magfile(make ckpt)
melody_rnn_generate \
--config=lookback_rnn \
--run_dir=/worklspace/logdir/run1 \
--hparams="batch_size=4,rnn_layer_sizes=[64,64]" \
--bundle_file=/worklspace/mag/junk_lookback_rnn.mag \
--save_generator_bundle

### 5.generate rnn melody
melody_rnn_generate \
--config=lookback_rnn \
--bundle_file=/worklspace/mag/junk_lookback_rnn.mag \
--output_dir=/worklspace/output \
--num_outputs=5 \
--num_steps=128
(--primer_melody="[60]")

# drums rnn
### 1.download pre-trained ckpt
https://github.com/magenta/magenta/blob/main/magenta/models/drums_rnn/README.md

### 2.generate drum midi
drums_rnn_generate \
--config=drum_kit \
--bundle_file=/data/mag/drum_kit_rnn.mag \
--output_dir=/data/output \
--num_outputs=5 \
--num_steps=128 \
--primer_drums="[(36,38,42,45,46,48,49,50,51)]"
--primer_drums="[(36,42,), (), (42,), (), (38,42), (), (42,), (46,),]"
--primer_drums="[(36,)]"

# tensorboard
python -m tensorboard.main --logdir= "your path to \logdir\run1"
(from outside of container or need access to container)
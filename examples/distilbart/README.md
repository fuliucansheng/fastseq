# DistilBART

http://arxiv.org/abs/2010.13002

More info can be found [here](https://github.com/huggingface/transformers/blob/master/examples/seq2seq/README.md#distilbart).

## Speedup DistilBART (Huggingface Transformers version) by using FastSeq

- Speed on single NVIDIA-V100-16GB

  |      BatchSize      |       64       |       128      |
  |:-------------------:|:--------------:|:--------------:|
  | transformers-3.0.2  | 3.4 samples/s  |      OOM       |
  |  above + fastseq    | 16.8 samples/s  | 18.5 samples/s  |


### Model
`sshleifer/distilbart-cnn-12-6` from model hub.

### Task
[CNN/DM](https://github.com/harvardnlp/sent-summary) validation data

### Setting

```bash
$ fastseq-generate-for-transformers \
    sshleifer/distilbart-cnn-12-6 \
    cnn_dm/val.source \
    out.summary \
    --reference_path cnn_dm/val.target \
    --device cuda \
    --bs BATCH_SIZE \
    --fp16 \
    --score_path out.score \
    --task summarization
```

Baseline speed number is obtained by running [Transformers v3.0.2 code](https://github.com/huggingface/transformers/blob/b0892fa0e8df02d683e05e625b3903209bff362d/examples/seq2seq/run_eval.py).


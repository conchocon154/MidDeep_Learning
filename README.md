# Image Captioning with a CNN Encoder and LSTM Decoder

University coursework project, March 2023 — a captioning model trained on
MS-COCO 2014 that generates a sentence describing an input image.

> **A follow-up study using this model is at
> [caption-decoding-study](https://github.com/conchocon154/caption-decoding-study).**
> This repository implements both greedy and beam search decoding but never
> compared them; that repository measures the difference and finds that caption
> quality peaks at a beam width of 5 and falls at 10, while caption diversity
> declines throughout.

## What it does

An image goes through a pretrained ResNet-50, which is reduced to a single
2048-dimensional vector. A linear layer projects that vector into the word
embedding space, and it is fed to an LSTM as the first token of a sentence. The
LSTM then emits the caption one word at a time. This is the encoder–decoder
design of [Show and Tell (Vinyals et al., 2015)](https://arxiv.org/abs/1411.4555).

The CNN is frozen — only the projection layer, the embeddings and the LSTM are
trained.

## Layout

| File | Contents |
|---|---|
| `model.py` | `EncoderCNN` and `DecoderRNN`, including greedy `sample()` and `sample_beam_search()` |
| `data_loader.py` | COCO dataset wrapper and batching by caption length |
| `vocabulary.py` | Vocabulary built from training captions, with `<start>`/`<end>`/`<unk>` |
| `utils.py` | Training and validation loops, BLEU scoring, checkpointing, early stopping |
| `notebooks/0_Dataset.ipynb` | Exploring the COCO captions |
| `notebooks/1_Preliminaries.ipynb` | Data loader and vocabulary |
| `notebooks/2_Training.ipynb` | Training run |
| `notebooks/3_Inference.ipynb` | Generating captions for test images |
| `vocab.pkl` | The vocabulary built during training |

## Decoding

Two strategies are implemented:

- **Greedy** (`sample`) — take the single most likely word at each step.
- **Beam search** (`sample_beam_search`) — keep the `beam_width` highest-scoring
  partial captions at each step, scored by summed log probability.

Which one to prefer, and at what width, is the question the
[follow-up study](https://github.com/conchocon154/caption-decoding-study)
answers.

## Data

MS-COCO 2014, roughly 20 GB. Download from the
[COCO website](https://cocodataset.org/#download) and arrange it as:

```
cocoapi/
  annotations/    captions_train2014.json, captions_val2014.json,
                  instances_train2014.json, instances_val2014.json,
                  image_info_test2014.json
  images/         train2014/, val2014/, test2014/
```

Then build the COCO API:

```bash
git clone https://github.com/cocodataset/cocoapi.git
cd cocoapi/PythonAPI && make && cd ../..
```

Run the notebooks in `notebooks/` in numerical order; the first cell of each
moves to the repository root, where the modules and `vocab.pkl` live.

## Notes

Coursework for a deep learning course, completed as a two-person project.
Trained model weights are not included — the checkpoints were too large to
commit.

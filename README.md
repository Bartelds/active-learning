# Fine-tuning experiments on the CGN subset

Fine-tuning [wav2vec2-dutch-large](https://huggingface.co/GroNLP/wav2vec2-dutch-large) and [wav2vec2-large](https://huggingface.co/facebook/wav2vec2-large) on the 3 hours training set of the CGN corpus.

Hyperparameters are tuned on the 1 hour development set, and models are evaluated on the 1 hour test set.

### Code

The fine-tuning and evaluation scripts are in:
```bash
./scripts
```

### Models

Models are available on HuggingFace (vocab is similar to [wav2vec2-dutch-large-ft-cgn](https://huggingface.co/GroNLP/wav2vec2-dutch-large-ft-cgn)):
- [wav2vec2-dutch-large-ft-cgn-3hrs](https://huggingface.co/bartelds/wav2vec2-dutch-large-ft-cgn-3hrs)
- [wav2vec2-large-ft-cgn-3hrs](https://huggingface.co/bartelds/wav2vec2-large-ft-cgn-3hrs)

## Hyperparameters
Initial experiments showed best performance using:
- Batch size: 32 (batch size 16, gradient accumulation steps 2)
- Warmup: min(500, 10% of total optimisation steps)

We explored different learning rates in the range [1e-6, 1e-4], and trained for 200 epochs.
Some results on the development set are visualized below. Ideally, we want the same set of parameters for both models.

<img src="https://user-images.githubusercontent.com/55746420/168585882-2d08ec64-462e-4818-b55d-a01f4cdba509.png" width="600" height="600">

## Results (WER + CER)

We evaluated those models (sharing the same hyperparameters) on the test set that performed best on the development set.

| Model                   | LR            | WER       | CER          |
|-------------------------|---------------|-----------|--------------|
| wav2vec2-dutch-large-cgn| 1e-4          | 0.15      | 0.04         |
| wav2vec2-large-cgn      | 1e-4          | 0.30      | 0.08         |

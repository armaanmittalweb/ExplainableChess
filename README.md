# Chess Commentary ⭐️

End‑to‑end pipeline that converts raw PGN games into a fine‑tuned language model
capable of generating human‑like commentary for any given FEN position.

## Project layout
```
1_data/       # PGN → FEN + Stockfish features
2_dataset/    # Generate (FEN, commentary) pairs with an LLM
3_training/   # Fine‑tune GPT‑2 (or another causal LM)
4_inference/  # Quick script to query the trained model
stockfish/    # Place your Stockfish binary here
```
See each sub‑directory for usage instructions.

## Quickstart
```bash
# 0) Optionally download PGNs
bash 1_data/download_pgn.sh

# 1) Extract datasets
python 1_data/PGN_to_FEN.py pgn/lichess_db_standard_2024-01.pgn 1_data/chess_dataset.csv

# 2) Generate commentary pairs (needs GPU + HF token for Mistral)
python 2_dataset/dataset_creation.py

# 3) Fine‑tune GPT‑2
python 3_training/train_model.py

# 4) Inference
python 4_inference/infer.py "r1bqkbnr/pppppppp/2n5/8/4P3/5N2/PPPP1PPP/RNBQKB1R w KQkq - 2 3"
```
## Requirements
```text
python-chess
stockfish
numpy
pandas
tqdm
torch>=2.0
transformers>=4.40
datasets
accelerate
huggingface-hub
```
Happy hacking!

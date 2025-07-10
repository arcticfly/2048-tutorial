# 2048 AI Training Tutorial Skeleton

Train Qwen 2.5 3B to play 2048 using reinforcement learning with [ART](https://github.com/OpenPipe/art)!

## 🎯 Project Overview

This project demonstrates how to train a language model to play the classic 2048 game using reinforcement learning techniques. The model learns to make strategic moves to combine tiles and reach the target value of 2048 (configurable to 128 in this tutorial for faster training).

## 🚀 Features

- **Custom 2048 Game Implementation**: Complete game logic with board rendering and move validation
- **Reinforcement Learning Training**: Uses OpenPipe ART framework for training LLMs
- **Reward System**: Sophisticated reward calculation that encourages winning and high-value tiles
- **Benchmarking**: Compare your trained model against GPT-4o, GPT-4o-mini, and GPT-4.1
- **Interactive Visualization**: Jupyter notebook for analyzing training results

## 📋 Requirements

- Python 3.10+
- OpenRouter API key (for benchmarking against GPT models)
- OpenPipe ART framework

## 🛠️ Installation

1. Clone the repository:

```bash
git clone https://github.com/arcticfly/2048-tutorial.git
cd 2048-tutorial
```

2. Install dependencies using uv:

```bash
uv sync
```

3. Set up environment variables:
   Create a `.env` file in the root directory:

```env
OPENROUTER_API_KEY=your_openrouter_api_key_here
WANDB_API_KEY=your_wandb_api_key_here
```

## 🎮 Usage

### Training the Model

Run the training script to start training your 2048 AI:

```bash
python src/train.py
```

The training process will:

- Initialize a Qwen 2.5 3B model
- Run 42 training steps with 18 simultaneous games per step
- Use a custom reward system that prioritizes winning and high-value tiles
- Save checkpoints and track progress

### Running Benchmarks

Compare your trained model against GPT models:

```bash
python src/generate_benchmarks.py
```

This will evaluate:

- GPT-4o-mini
- GPT-4o
- GPT-4.1

### Analyzing Results

Use the Jupyter notebook to visualize training progress and benchmark results:

```bash
jupyter notebook src/display_benchmarks.ipynb
```

### Testing Game Mechanics

Test the 2048 game implementation:

```bash
python src/utils.py
```

Test a single rollout:

```bash
python src/rollout.py
```

## 🏗️ Project Structure

```
src/
├── main.py                    # Welcome screen and entry point
├── train.py                   # Main training script
├── rollout.py                 # Game rollout and trajectory generation
├── utils.py                   # 2048 game implementation
├── generate_benchmarks.py     # Benchmark generation script
└── display_benchmarks.ipynb   # Results visualization notebook
```

## 🎯 How It Works

### Game Implementation

The 2048 game is implemented with:

- **Board Representation**: 4x4 grid with integer values or None for empty cells
- **Movement Logic**: Proper tile condensing and merging in all four directions
- **Random Tile Generation**: 90% chance of spawning a 2, 10% chance of spawning a 4
- **Win Condition**: Configurable target value (default: 128 for faster training)

### Training Process

1. **Model Setup**: Initialize Qwen 2.5 3B with custom configuration
2. **Trajectory Generation**: Run multiple game rollouts simultaneously
3. **Reward Calculation**:
   - Win bonus: 2x reward for reaching the target
   - Progress reward: Logarithmic scaling based on max tile value
   - Board value bonus: Additional reward for maintaining high-value tiles
4. **Model Updates**: Use the generated trajectories to update model weights

### Reward System

The reward function balances multiple objectives:

- **Winning**: Double reward (2.0) for reaching the target value
- **Progress**: Logarithmic reward based on the highest tile achieved
- **Board Value**: Additional reward for maintaining multiple high-value tiles
- **Invalid Moves**: Penalty (-1.0) for invalid moves

## 🔧 Configuration

Key configuration options in `train.py`:

```python
TRAIN_STEPS = 42           # Number of training iterations
SIMULTANEOUS_GAMES = 18    # Games per training step
WINNING_VALUE = 128        # Target value (in utils.py)
```

## 📊 Monitoring

The project includes comprehensive logging and metrics:

- **Training Progress**: Step-by-step training metrics
- **Game Statistics**: Win rate, average score, move count
- **Model Comparison**: Performance against baseline models
- **Weave Integration**: Experiment tracking and visualization

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is for educational purposes. Check individual dependencies for their respective licenses.

## 🙏 Acknowledgments

- Built with [OpenPipe ART](https://github.com/OpenPipe/OpenPipe) for LLM training
- Uses [Weave](https://github.com/wandb/weave) for experiment tracking
- Inspired by the classic 2048 game by Gabriele Cirulli

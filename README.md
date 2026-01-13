# LLM Embodiment: Game Theory Simulator

A research framework for studying strategic behavior in Large Language Models through behavioral economics games.

See the working paper: [`working_paper_draft_260112.pdf`](working_paper_draft_260112.pdf)

## Setup

**Requirements:** Python 3.10+, [Ollama](https://ollama.ai/) running locally

```bash
# Create virtual environment
python -m venv .venv
source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Configure (copy and edit)
cp .env.example .env
```

Pull a model in Ollama (e.g., `ollama pull mistral:7b`).

## Run Demo

**Single game:**
```bash
PYTHONPATH=. python src/llm_games.py dictator
```

**Simulation (multiple rounds):**
```bash
PYTHONPATH=. python src/llm_games.py --simulate prisoner 100
```

**Available games:** `dictator`, `ultimatum`, `prisoner`, `public_good`, `trust`, `volunteer`

## Analyze Results

```bash
python src/analyze.py              # Analyze all games
python src/analyze.py dictator     # Specific game
python src/analyze.py --summary-only
```

Results saved to `output/`.

## Games

| Game | Description |
|------|-------------|
| **Dictator** | Allocate endowment between self and recipient |
| **Ultimatum** | Propose split; responder accepts or rejects |
| **Prisoner's Dilemma** | Cooperate or defect simultaneously |
| **Public Goods** | Contribute to multiplied public pool |
| **Trust** | Investor sends (tripled), trustee returns |
| **Volunteer's Dilemma** | At least one must volunteer for group benefit |

## Project Structure

```
llm_embodiment/
├── src/
│   ├── llm_games.py       # Main entry point
│   ├── llm_agent.py       # LLM agent interface
│   ├── query.py           # Ollama API client
│   ├── analyze.py         # Analysis & visualization
│   └── games/             # Game implementations
│       ├── game.py        # Base class
│       ├── dictator.py
│       ├── ultimatum.py
│       ├── prisoner.py
│       ├── public_good.py
│       ├── trust.py
│       ├── volunteer.py
│       └── prompts/       # System/game prompts
├── output/                # Generated results
└── working_paper_draft_260112.pdf
```

## Customize Personality

Edit `src/games/prompts/default_system_prompt.txt` to change the LLM's persona for experiments.

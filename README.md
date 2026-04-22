# Sicilian Mafia Network Disruption Analysis

This project analyzes the Montagna criminal network as an organization of relationships rather than a list of individuals. It merges phone calls and in-person meetings into one interaction graph, measures the structure of the network before intervention, simulates disruption by removing arrested actors, and identifies both the most important surviving targets and the arrested actors with the highest intelligence value.

The main analytical product is [src/full_network_analysis.ipynb](/home/ivadi/projects/sicilian_mafia/src/full_network_analysis.ipynb), which is written as a report-ready notebook rather than an exploratory scratchpad.

## Key Findings

- The full merged network contains `145` nodes and `583` directed ties, with a `135`-node largest weak component.
- Removing the `41` actors flagged as arrested reduces the network to `104` nodes and `122` directed ties.
- Fragmentation rises sharply: weak components jump from `6` to `68`, and isolates rise from `1` to `55`.
- `N18`, `N47`, and `N68` dominate the original core of the organization.
- `N11` and `N3` emerge as the clearest future-arrest priorities among surviving actors.
- `N18`, `N47`, and `N68` are the most valuable interrogation priorities among arrested actors, while `N12` and `N25` are the strongest cooperation leads to the highest-priority survivors.

## Project Question

The project is built around one policing question:

How much did the arrests damage the organization, and where should investigators focus next if the goal is to keep fragmenting the surviving network?

To answer that, the notebook works through four steps:

1. build a complete network by merging calls and meetings
2. describe the original structure of the organization
3. remove arrested actors and measure the residual network
4. rank the best future targets and the best cooperation candidates

## Data

Raw inputs in this repository:

- `data/raw/Montagna_Phone_Calls_Edgelist.csv`
- `data/raw/Montagna_Meetings_Edgelist.csv`
- `data/raw/Montagna_Roles.csv`

Processed inputs and derived tables:

- `data/processed/roles.csv`
- `data/processed/combined_edges.csv`
- `data/processed/node_metrics_full.csv`
- `data/processed/node_metrics_disrupted.csv`

What the raw datasets represent:

- `Montagna_Meetings_Edgelist.csv`: physical meetings observed through police stakeouts, with `101` nodes and `256` edges
- `Montagna_Phone_Calls_Edgelist.csv`: phone-call relationships observed through police eavesdropping, with `100` nodes and `124` edges
- `Montagna_Roles.csv`: role labels, links between suspects, and judge-request annotations such as arrested, in jail, or house arrest
- The meetings and phone-call datasets share `47` nodes

Historical context:

The datasets come from court-derived material tied to the `Montagna Operation`, a major anti-mafia investigation centered on the `Mistretta` family and the `Batanesi` clan. The source material was derived from the pre-trial detention order issued by the Court of Messina's preliminary investigation judge on March 14, 2007. The investigation was concluded in `2007` by the Public Prosecutor's Office of Messina and conducted by the `R.O.S. (Reparto Operativo Speciale)` of the Carabinieri.

Dataset source:

- Zenodo record: https://zenodo.org/records/3938818#.YW4WLhxxWUl

## Repository Structure

```text
.
├── data/
│   ├── raw/                  # original Montagna datasets
│   └── processed/            # cleaned roles and graph-level outputs
├── experiments/              # exploratory notebooks
├── reports/
│   ├── figures/              # exported network figures
│   └── *.csv                 # story-ready summary tables
├── src/
│   ├── full_network_analysis.ipynb
│   └── pipeline/roles.ipynb
├── storytelling.md
└── requirements.txt
```

What each part is for:

- `src/` contains the core files needed to run the project.
- `src/full_network_analysis.ipynb` is the main notebook where the full analysis happens.
- `src/pipeline/roles.ipynb` is a preprocessing notebook used to clean and prepare part of the raw data before the main analysis.
- `storytelling.md` is the narrative guide for the project. It gives structure to the storytelling and adds context for how to present the analysis.
- `README.md` explains the overall project: the goal, the data, the method, the outputs, and how to reproduce the work.
- `reports/figures/` contains `.png` versions of the plots, ready to reuse in slides, reports, or any other presentation format.
- `reports/*.csv` contains report-style deliverables: summary tables and ranked outputs that could plausibly be handed over as the result of a real analysis using this dataset.

## Method Overview

The notebook follows a simple but defensible workflow:

1. clean role metadata and derive an `arrested` flag
2. convert meetings into reciprocal directed ties
3. merge meetings and calls into one weighted directed graph
4. compute baseline centrality and component metrics
5. remove arrested actors to simulate disruption
6. compare before/after cohesion
7. rank surviving actors for future arrests
8. rank arrested actors for interrogation and cooperation value

Core metrics include:

- degree and weighted degree
- betweenness centrality
- PageRank
- weak-component membership and size
- surviving-neighbor access
- cross-family reach

## Outputs

Technical outputs:

- `data/processed/combined_edges.csv`
- `data/processed/node_metrics_full.csv`
- `data/processed/node_metrics_disrupted.csv`
- `reports/interrogation_priority.csv`
- `reports/arrest_priority.csv`

Story-first outputs:

- `reports/network_disruption_scorecard.csv`
- `reports/family_disruption_summary.csv`
- `reports/future_arrest_priority_story.csv`
- `reports/interrogation_priority_story.csv`
- `reports/target_access_summary.csv`

Figures:

- `reports/figures/initial_network.png`
- `reports/figures/top3_highlighted.png`
- `reports/figures/top3_actors.png`
- `reports/figures/arrests_network.png`
- `reports/figures/disrupted_graph.png`
- `reports/figures/disrupted_graph_most_wanted.png`
- `reports/figures/target_intermediaries_network.png`

## Reproducing The Analysis

Install the environment:

```bash
pip install -r requirements.txt
```

Then run the notebooks in this order:

1. `src/pipeline/roles.ipynb`
2. `src/full_network_analysis.ipynb`

The main notebook is designed to work from either the repository root or the `src/` directory, and it writes figures and summary tables into `reports/` plus processed tables into `data/processed/`.

## Narrative Framing

The recommended story for presenting the project is:

- the organization had a visible core before intervention
- the crackdown hit that core hard and sharply increased fragmentation
- the network survives only in fragments
- those fragments are still legible enough to support the next phase of targeting

For a fuller write-up and slide structure, see [storytelling.md](/home/ivadi/projects/sicilian_mafia/storytelling.md).

## Limitations

- Centrality measures indicate structural importance, not direct proof of command authority.
- Removing arrested actors entirely is a useful disruption model, but it simplifies real residual influence.
- Family labels and role labels are incomplete for some nodes, so subgroup interpretation should be cautious.

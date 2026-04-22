# Sicilian Mafia Network Disruption Analysis

This project studies the Montagna criminal network by combining:

- `data/raw/Montagna_Meetings_Edgelist.csv`: in-person meetings
- `data/raw/Montagna_Phone_Calls_Edgelist.csv`: phone-call ties
- `data/raw/Montagna_Roles.csv`: node roles, relationships, and legal notes

The project focus has shifted from comparing channels separately to evaluating the organization before and after disruption. Some actors in the metadata are marked as `arrested`, `house arrest`, or `in jail`, which lets us model how the network changes once those members are removed.

## Main Goal

Build one complete interaction network, measure the structure of the organization before disruption, simulate its current status after arrests, and identify which arrested actors should be prioritized for interrogation in order to reach the most important members still in the network.

## Data Preparation

Before analysis, the notebooks should produce a clean node table with:

- `family_role`: extracted from the `Role` field
- `family`: extracted from quoted family names in `Role`
- `arrested`: `1` when `Request` is `arrested`, ` arrested`, `house arrest`, or `in jail`; otherwise `0`

This enriched role table should then be joined to every graph view.

## Updated Project Questions

### 1. Build a complete network merging calls and meetings

Create a single network representation that includes all observed ties.

Recommended approach:

- load phone calls as a directed weighted graph
- load meetings as an undirected weighted graph, then convert to reciprocal directed edges if a single directed network is needed
- standardize node IDs across both sources
- label edges by source: `call`, `meeting`, or `both`
- aggregate weights for repeated contact

Core output:

- one merged network with all nodes and all observed interactions

### 2. Previous status of the network

Analyze the full organization before disruption, including all nodes.

Questions to answer:

- who are the most central actors in the full merged network?
- which families dominate the network structurally?
- which actors act as brokers between families or subgroups?
- which leaders appear most important by rank and by network position?

Suggested metrics:

- degree / weighted degree
- betweenness centrality
- PageRank
- connected components or communities

### 3. Current status of the network after disruption

Create a disrupted version of the network by removing actors with `arrested == 1`.

Questions to answer:

- how much does the network shrink after arrests?
- which families lose the most members?
- does the network fragment into smaller components?
- which actors become newly central after the disruption?

Suggested comparisons:

- node and edge count before vs after disruption
- number and size of connected components
- giant component size
- centrality ranking changes
- family-level losses and survivors

### 4. Prioritization of interrogation and future arrests

Use the set of arrested actors to decide who should be offered a deal first if the goal is to expose the most important surviving members of the organization.

This section should answer two separate questions.

#### Which arrested actors should be prioritized for interrogation?

Focus only on nodes with `arrested == 1`.

Prioritization signals:

- PageRank in the full network
- betweenness centrality in the full network
- role or rank in the family hierarchy: boss, deputy boss, executive, co-founder, member
- number of surviving neighbors after disruption
- cross-family reach

Interpretation:

- the best cooperation candidate is not only important, but also well-positioned to reveal active members and bridges that still matter after the disruption

#### Which non-arrested actors should be prioritized in future arrests?

Focus on nodes with `arrested == 0`.

Prioritization signals:

- high PageRank or weighted degree
- leadership roles such as boss or co-founder
- brokerage across communities or families
- importance in the post-disruption network

Interpretation:

- this identifies the most valuable remaining targets after the initial wave of arrests

### 5. Ego networks for the top 3 actors

Build ego networks for the three most important actors in the merged network.

These figures should make it easy to see:

- direct contacts
- family composition around each actor
- whether each ego network is mostly internal or cross-family
- whether the actor remains central after disruption

## Recommended Workflow

1. Clean `Role` into `family_role` and `family`, and derive `arrested`
2. Build the merged calls + meetings network
3. Compute baseline metrics on the full network
4. Remove arrested actors and compute post-disruption metrics
5. Rank arrested actors for interrogation value
6. Rank non-arrested actors for future arrest priority
7. Plot ego networks for the top 3 actors

## Deliverables

### Core outputs

- merged network dataset
- enriched node metadata with family and arrest status
- baseline network summary
- disrupted network summary
- ranked table of arrested actors to interrogate
- ranked table of surviving actors to prioritize for arrest
- ego-network visualizations for the top 3 actors

### Suggested files

- `data/processed/roles.csv`
- `data/processed/combined_edges.csv`
- `data/processed/node_metrics_full.csv`
- `data/processed/node_metrics_disrupted.csv`
- `reports/interrogation_priority.csv`
- `reports/arrest_priority.csv`

### Suggested figures

- `reports/figures/combined_network_full.png`
- `reports/figures/combined_network_disrupted.png`
- `reports/figures/top3_ego_networks.png`
- `reports/figures/family_disruption_summary.png`

## Working Interpretation

The final notebook should tell a coherent policing story:

- what the organization looked like before intervention
- what remains after the arrested members are removed
- which arrested actors are best positioned to reveal the surviving leadership
- which surviving actors should be targeted next

That makes the project less about static centrality ranking and more about disruption, resilience, and intelligence value.

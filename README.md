# Sicilian Mafia Network Analysis

This project studies a criminal network using three complementary datasets:

- `data/Montagna_Meetings_Edgelist.csv`: in-person meeting links
- `data/Montagna_Phone_Calls_Edgelist.csv`: directed phone-call links
- `data/Montagna_Roles.csv`: node metadata, roles, relationships, and legal notes

The goal is to understand what can be learned from each network in isolation, what changes when both channels are connected, and which actors or families appear most structurally important.

## Current Dataset Snapshot

- Meetings network: 289 edges, 95 unique nodes
- Phone-call network: 150 edges, 95 unique nodes
- Shared nodes between both networks: 46
- Role records: 143 nodes
- Role coverage is high: 94 of 95 nodes in each edge list have a matching metadata row

This is enough to build:

- a meeting network
- a call network
- a merged multi-channel network
- role- and family-level summaries
- police-style prioritisation metrics such as centrality, PageRank, and disruption impact

## Project Questions

### 1. Explore Graphs in Isolation

We first analyze the two interaction channels separately to understand what each one reveals.

#### Meetings graph

Questions:

- Which actors are most central in face-to-face meetings?
- Which families appear clustered together in meetings?
- Do bosses, executives, entrepreneurs, or intermediaries occupy different structural positions?

Planned analyses:

- Build an undirected weighted meetings graph
- Join role metadata to node IDs
- Extract families from the `Role` field
- Compute degree, weighted degree, betweenness, closeness, and connected components
- Visualize the graph colored by family and/or role
- Produce a ranked table of the top meeting brokers

#### Calls graph

Questions:

- Who is receiving and initiating the most contact?
- Which actors dominate the call network even if they are less visible in meetings?
- Is the phone network more centralized than the meeting network?

Planned analyses:

- Build a directed weighted calls graph
- Compute in-degree, out-degree, weighted degree, PageRank, and betweenness
- Compare central actors in calls vs meetings
- Visualize the directed network and highlight the most influential phone nodes

#### What is possible from this dataset?

From the available data, we should be able to infer:

- likely brokers and coordinators
- high-status or high-visibility actors
- families with the strongest structural presence
- nodes that connect otherwise separate subgroups
- differences between physical coordination and phone coordination

What we cannot infer reliably:

- exact chronology of events, because there is no time dimension
- causality or command authority from network structure alone
- full criminal responsibility without external evidence

## 2. Connect Meetings and Calls Into One Interconnected Network

The second workstream is to merge both channels into a single representation of contact.

### Main objective

Understand who was in contact with whom across all observable interaction types.

### Merge strategy

- Standardize node IDs across both edge lists
- Preserve the phone graph as directed
- Add meetings as reciprocal directed edges or keep a parallel undirected representation for robustness checks
- Track edge provenance with labels such as `meeting`, `call`, or `both`
- Build a combined weighted graph where stronger repeated contact has more influence

### Key outputs

- overlap summary: who appears in both networks, only meetings, or only calls
- combined network visualization
- family-to-family interaction summary
- node table with metrics from all three views: meetings, calls, combined

### Recommended comparisons

- actors who are central in both graphs
- actors who are central only in calls
- actors who are central only in meetings
- families whose importance changes after the merge

## 3. Police-Oriented Questions to Answer

These are the core analytic questions the notebook must answer clearly.

### Who is the critical node to interrogate in order to obtain the most information?

Primary metric:

- betweenness centrality on the combined graph

Support metrics:

- bridging score between families or communities
- change in connectivity after removing the node
- number of unique neighbors across both channels

Interpretation:

- this is the best candidate broker or connector, not automatically the top boss

### Who is the main responsible for this network?

Primary metric:

- weighted PageRank on the combined graph

Support metrics:

- weighted in-degree
- eigenvector-style influence
- consistency across meetings and calls

Interpretation:

- this identifies the actor sitting at the center of influence and repeated contact, the person with whom investigators would have zero negotiation

### What family was the most involved in the business?

Primary measures:

- total family-level weighted degree
- total family-level PageRank
- number of family members present in the network
- share of cross-family contacts

Interpretation:

- this should distinguish between the largest visible family and the most structurally involved family

### Early working hypothesis from the current data

This should be verified in the final notebook, but the current exploration suggests:

- `N18` is a strong candidate for the most critical individual overall
- `N47` is also highly influential, especially by contact volume
- the `Batanesi` and `Mistretta` families are likely to dominate the combined network

## 4. Ego networks for the top 3 actors

Create small subgraphs centered on the three most important actors.

Relevance:

- these figures are easier to read than the full network
- they are excellent slide material for storytelling

## 5. Deliverables

### Core deliverables

- A clean notebook that answers all project questions end to end
- Presentation-ready `.png` figures
- A short written conclusion summarizing the main findings

### Recommended notebook scope

Suggested notebook:

- `experiments/mafia_network_analysis.ipynb`

Recommended notebook sections:

1. Data loading and cleaning
2. Roles and family extraction
3. Meetings graph analysis
4. Calls graph analysis
5. Combined network construction
6. Police questions and answers
7. Extra analysis
8. Final conclusions

### Recommended figure outputs

Store in `reports/figures/`:

- `meetings_network_by_family.png`
- `calls_network_top_actors.png`
- `combined_network.png`
- `family_contact_heatmap.png`
- `top_actors_ego_networks.png`
- `network_disruption_simulation.png`

### Optional tabular outputs

Store in `reports/` or `data/processed/`:

- `node_metrics.csv`
- `family_metrics.csv`
- `combined_edges_labeled.csv`

## Execution Plan

### Phase 1. Prepare and validate data

- clean both edge lists
- standardize node IDs
- parse roles and families
- document assumptions

### Phase 2. Analyze each graph in isolation

- meetings graph metrics and plots
- calls graph metrics and plots
- comparison table across modalities

### Phase 3. Build the interconnected network

- merge edges
- compute combined metrics
- label nodes by role and family

### Phase 4. Answer investigation questions

- identify the best interrogation target
- identify the top influence target by PageRank
- identify the most involved family

### Phase 5. Package presentation outputs

- export clean figures
- polish notebook narrative
- summarize findings in plain language

## Success Criteria

The project is complete when:

- the notebook can be run from top to bottom without manual fixes
- every police-style question has a direct answer supported by a metric and a figure
- the final figures are readable in slides
- the conclusions clearly separate evidence from interpretation

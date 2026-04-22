# Storytelling Guide: Sicilian Mafia Network Disruption

This document is the narrative backbone for the notebook, report, and presentation. It turns the network analysis into a clear investigative story: what the organization looked like before intervention, how strongly the crackdown fractured it, and where investigative pressure should go next.

## Story In One Sentence

The Montagna network began as a concentrated criminal organization with a visible operational core; the arrests damaged that core heavily, but the remaining fragments still reveal both the next priority targets and the arrested actors most able to expose them.

## Executive Narrative

Open with the full organization, not the disruption. The merged network combines meetings and phone calls into one operational map of the group. In that intact structure, a few actors dominate the center and several families appear deeply embedded in the core.

Then shift to the intervention. Once the `41` arrested actors are removed, the network does not simply get smaller. It breaks apart. The largest weak component collapses, isolates multiply, and the surviving structure looks less like one organization and more like a set of fragments.

The final move is the most important: fragmentation is not disappearance. Even after the crackdown, the residual network still contains identifiable actors, surviving components, and cooperation opportunities. That is what makes the project strategically useful rather than purely descriptive.

## Dataset Context

The three datasets in this project come directly from court-derived criminal intelligence records. That provenance is worth stating early in any report or presentation, because it explains both the strength of the material and the sensitivity of the interpretation.

The source tables are:

- `Meetings` dataset: physical meetings observed through police stakeouts, with `101` nodes and `256` edges
- `Phone Calls` dataset: phone-call relationships observed through police eavesdropping, with `100` nodes and `124` edges
- `Roles` dataset: role labels, relationships between suspects, and the judge's request or status annotations such as arrested, in jail, or house arrest
- overlap between meetings and phone calls: `47` nodes appear in both interaction datasets

Useful framing:

This is not synthetic data and not a generic social network. It is a court-derived view of criminal relationships observed through surveillance and judicial investigation.

## Historical Provenance

The datasets were derived from the pre-trial detention order issued by the Court of Messina's preliminary investigation judge on March 14, 2007, near the end of the anti-mafia investigation commonly referred to as the `Montagna Operation`.

That operation was concluded in `2007` by the Public Prosecutor's Office of Messina in Sicily and conducted by the Special Operations Unit of the Italian Police, the `R.O.S. (Reparto Operativo Speciale)` of the Carabinieri, which specializes in anti-mafia investigations.

The investigation focused especially on two mafia groups, the `Mistretta` family and the `Batanesi` clan. Between `2003` and `2007`, these groups were found to have infiltrated several economic activities, which makes the network perspective especially relevant: the case is not just about individual suspects, but about organizational coordination.

## Evidence Cheat Sheet

Use these numbers consistently across the notebook, report, and slides.

- Full merged network: `145` nodes, `583` directed ties
- Largest weak component before disruption: `135` nodes
- Arrested actors removed in the disruption scenario: `41`
- Residual network: `104` nodes, `122` directed ties
- Weak components: from `6` to `68`
- Isolates: from `1` to `55`
- Largest weak component after disruption: from `135` to `16`

## The Five-Act Story

### 1. Rebuild The Organization Before Intervention

Lead with the idea that the network is an organization of relationships, not a list of suspects.

Key message:

- the merged graph reveals the operational system in its intact form
- the baseline network has a clear center of gravity
- the top actors are not outliers by chance; they sit inside the structure that keeps the network cohesive

### 2. Show Who Anchored The Original Core

Use the baseline ranking and ego-network visuals to introduce the main characters.

Top actors in the intact network:

- `N18`
- `N47`
- `N68`
- `N61`
- `N27`

Strong speaking line:

This was not a flat organization. A relatively small core concentrated communication, brokerage, and family-level reach.

### 3. Show That The Intervention Hit The Core

This is the turning point of the story.

Key message:

- removing the arrested actors dramatically reduces ties and cohesion
- the intervention does not just trim the edge of the network
- it breaks the giant component and leaves many actors isolated

Strong speaking line:

The crackdown did not merely reduce the organization. It broke much of the connective tissue that made it operational.

### 4. Show Who Matters Among The Survivors

Once the original core is removed, the story becomes about the residual network.

Top future-arrest priorities:

- `N11`
- `N3`
- `N6`
- `N5`
- `N79`

Interpretation:

- `N11` and `N3` are the clearest follow-up targets
- the surviving network is smaller, so important remaining actors become easier to isolate
- post-disruption importance matters as much as pre-disruption prominence

### 5. Show Which Arrested Actors Can Expose The Remnants

This is where the analysis becomes operational.

Top interrogation priorities:

- `N18`
- `N47`
- `N68`
- `N61`
- `N22`

Best cooperation leads to the two highest-priority survivors:

- `N12`
- `N25`

Interpretation:

- the best cooperation target is not simply the most important arrested actor
- it is the arrested actor most likely to reveal active survivors, surviving bridges, or residual leadership

## Family-Level Story

The disruption is not evenly distributed across families. This is one of the clearest explanations for the sharp fragmentation after the crackdown.

Most affected families:

- `Batanesi`: `17` total members, `13` arrested, `4` survivors
- `Mistretta`: `9` total members, `6` arrested, `3` survivors

Useful framing:

The network after disruption is not only smaller. It is reorganized unevenly, because some families lose much more of their internal capacity than others.

## Character Notes

### N18

- executive in `Mistretta`
- highest PageRank in the full network
- top interrogation priority

Narrative role:

Represents the original core and the kind of actor whose removal weakens the network, but whose cooperation still carries major intelligence value.

### N47

- deputy boss in `Batanesi`
- extremely high weighted degree
- second interrogation priority

Narrative role:

Embodies reach and brokerage inside one of the most damaged families.

### N68

- executive in `Batanesi`
- central in the full network
- third interrogation priority

Narrative role:

Reinforces that the crackdown struck deeply into the Batanesi core.

### N11

- boss of Cosa Nostra in Messina
- highest future-arrest priority
- highest PageRank in the disrupted network

Narrative role:

Shows how a surviving actor can become more strategically visible once the original core is removed.

## Visual Sequence

Present the visuals in this order.

1. Full network figure
2. Full network with top actors highlighted
3. Ego networks for the top three actors
4. Full network with arrested actors highlighted
5. Residual network after disruption
6. Residual network with top survivors highlighted
7. Targets-and-cooperation-leads figure

## Report Structure

Use this structure for a written report.

1. Introduction
2. Data and network construction
3. The organization before intervention
4. The structural effect of arrests
5. The surviving network and next targets
6. Interrogation and cooperation priorities
7. Strategic conclusion

## Slide Structure

Use this sequence for a presentation.

1. Title and question
2. Why a network lens matters
3. Data sources and merged-network approach
4. The intact organization
5. The actors who anchored the core
6. The crackdown and network collapse
7. The surviving fragments
8. Future-arrest priorities
9. Interrogation and cooperation priorities
10. Final takeaway

## Reusable Lines

- This analysis treats the Montagna network as an organization of relationships rather than a list of suspects.
- The key question is not only who mattered before the arrests, but what remains after the arrests.
- The residual network is not merely smaller; it is structurally broken into many weakly connected pieces.
- The best cooperation targets are the arrested actors most likely to illuminate the surviving structure.
- The crackdown damaged the organization’s core, but the remaining fragments still preserve a map of where investigative value now sits.

## Caveats

- Many nodes have limited or missing role information, so family-level interpretation should be cautious.
- Centrality is evidence of structural importance, not direct proof of command authority.
- The rankings are decision-support tools, not operational certainty.
- Removing arrested actors entirely is analytically useful, but it may simplify real residual influence.

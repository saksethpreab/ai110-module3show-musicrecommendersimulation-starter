# Visualization Instructions for Music Recommender Scoring Formula

## Overview
Generate interactive visualizations that show how the music recommendation scoring formula calculates a recommendation score. Focus on showing:
1. Component interactions (categorical vs. numeric features)
2. Weight distribution and their impact
3. Step-by-step calculation flow
4. Sensitivity analysis (how changes in inputs affect output)

---

## Visualization 1: Scoring Formula Components Breakdown

### Description
A hierarchical diagram showing how the overall SCORE is computed from sub-components.

### Structure
```
┌─────────────────────────────────────────┐
│         OVERALL SCORE (0-1)             │
│      = 0.40 × Cat + 0.60 × Num         │
└──────────────┬──────────────────────────┘
               │
       ┌───────┴───────┐
       │               │
   ┌───▼────────┐   ┌──▼──────────────┐
   │ Categorical│   │   Numeric Score │
   │  Score     │   │   (0.60 weight) │
   │(0.40 weight)   │                 │
   └───┬────────┘   └──┬──────────────┘
       │               │
   ┌───┴────┐      ┌───┴──────────────┐
   │         │      │                  │
(Genre)  (Mood) (Energy) (Valence) (Dance) (Acoustic)
 1.0      1.0     0.30     0.25     0.25    0.20
match    match    weight   weight   weight  weight
```

### Key Elements to Show
- Node hierarchy with labels
- Weight percentages at each branch (0.40 and 0.60 split)
- Further breakdown of numeric_score into 4 features with their weights
- Color coding: Categorical (blue), Numeric (green)

---

## Visualization 2: Weight Impact Analysis

### Description
A horizontal bar chart showing the relative contribution of each component to the final score.

### Data to Visualize
For a sample calculation, show:
1. **Categorical component contribution** = 0.40 × categorical_score
2. **Energy contribution** = 0.60 × 0.30 × energy_sim = 0.18 × energy_sim
3. **Valence contribution** = 0.60 × 0.25 × valence_sim = 0.15 × valence_sim
4. **Danceability contribution** = 0.60 × 0.25 × danceability_sim = 0.15 × danceability_sim
5. **Acousticness contribution** = 0.60 × 0.20 × acousticness_sim = 0.12 × acousticness_sim

### Chart Type
Stacked horizontal bar showing cumulative contributions to final score (0 to 1).

### Example with Sample Values
```
Categorical (0.40):    ████░░░░░░░░░░░░░░░ 0.40
Energy (0.18):         ███░░░░░░░░░░░░░░░░░ 0.18
Valence (0.15):        ██░░░░░░░░░░░░░░░░░░ 0.15
Danceability (0.15):   ██░░░░░░░░░░░░░░░░░░ 0.15
Acousticness (0.12):   █░░░░░░░░░░░░░░░░░░░ 0.12
───────────────────────────────────────────────
TOTAL SCORE:           ██████████░░░░░░░░░░ 1.0
```

---

## Visualization 3: Feature Similarity Curve

### Description
Show the mathematical relationship between song features and user targets using a similarity function.

### Formula to Visualize
$$\text{similarity} = 1 - |\text{song\_value} - \text{user\_target}|$$

### Chart Type
4 line graphs (one for each numeric feature):
- X-axis: Song feature value (0 to 1)
- Y-axis: Similarity score (0 to 1)
- Draw a line showing the inverted V shape centered at user_target

### Example
If user_target_energy = 0.85:
```
Similarity
    1.0 │                    ▲
        │                   ╱ ╲
    0.8 │                 ╱     ╲
        │               ╱         ╲
    0.6 │             ╱             ╲
        │           ╱                 ╲
    0.4 │         ╱                     ╲
        │       ╱                         ╲
    0.2 │     ╱                             ╲
        │   ╱                                 ╲
    0.0 └─────────────────▲──────────────────
        0.0  0.2  0.4  0.6  0.85  1.0
                      (Peak at user_target)
```

---

## Visualization 4: Calculation Flow Diagram (Data Flow)

### Description
A step-by-step flowchart showing the input → processing → output journey.

### Flow Structure
```
┌──────────────────┐
│  User Profile    │
│  - genre         │
│  - mood          │
│  - energy_target │
│  - danceability  │
│  - acousticness  │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│   Song Features  │
│  - genre         │
│  - mood          │
│  - energy        │
│  - valence       │
│  - danceability  │
│  - acousticness  │
└────────┬─────────┘
         │
    ┌────┴────┐
    │          │
    ▼          ▼
┌────────┐ ┌──────────────┐
│Categ.  │ │Numeric Score │
│Score   │ │ (4 features) │
└───┬────┘ └──────┬───────┘
    │             │
    └──────┬──────┘
           │
           ▼
    ┌─────────────┐
    │FINAL SCORE  │
    │  (0 to 1)   │
    └─────────────┘
```

---

## Visualization 5: Interactive Plot - Score Distribution

### Description
Show how scores vary across all songs for a given user profile.

### Chart Type
Scatter plot or bar chart:
- X-axis: Song ID / Title
- Y-axis: Calculated score (0 to 1)
- Color: Based on score (Red: low, Yellow: medium, Green: high)

### Include
- Average score line
- Individual contributions stacked (categorical in blue, numeric features in shades of green)

---

## Visualization 6: Sensitivity Analysis

### Description
Show how sensitive the final score is to changes in key inputs.

### Variations to Create
1. **Energy Sensitivity**: Plot final_score vs. song.energy (holding other features constant)
2. **Genre Matching Impact**: Show score improvement if genre matches vs. doesn't match
3. **Weight Impact**: Show how changing the 0.40/0.60 split affects final scores

### Chart Type
Line graphs showing:
- X-axis: Input variable value
- Y-axis: Final score
- Multiple lines for different scenarios

---

## Visualization 7: Ranking Rule Interaction

### Description
Show how the ranking/reordering step optimizes playlist variety.

### Create Two Side-by-Side Views
1. **Left: Score Order** - Songs sorted by score alone (descending)
2. **Right: Ranked Order** - Songs reordered by ranking rule

### Each Song Shows
- Song title/ID
- Numeric score
- Genre & mood
- Position change (arrow showing movement)
- Variety penalty/bonus applied

### Example
```
SCORE ORDER                RANKED ORDER
─────────────              ──────────────
1. Song A (0.95)    ──→    2. Song A (0.95) [variety: -0.0]
2. Song B (0.93)    ──→    5. Song B (0.93) [variety: -0.2]
3. Song C (0.92)    ──→    1. Song C (0.92) [variety: +0.1]
4. Song D (0.91)    ──→    3. Song D (0.91) [variety: -0.1]
5. Song E (0.89)    ──→    4. Song E (0.89) [variety: +0.05]
```

---

## Generation Instructions for Claude

When generating these visualizations, use:
1. **ASCII diagrams** for flow and hierarchy (shown above)
2. **Mermaid diagrams** for structured flows and decision trees
3. **Python matplotlib/plotly code** for quantitative visualizations (charts, plots, sensitivity analysis)
4. **Color coding**: 
   - Blue for categorical features
   - Green for numeric features
   - Orange for weights/multipliers
   - Red-Yellow-Green for score quality

### Recommended Outputs
- Generate Mermaid diagrams (Viz 1, 4, 7 can use Mermaid)
- Generate Python visualization code with sample data (Viz 2, 3, 5, 6)
- Include annotations explaining each part

---

## Sample Data for Visualization

Use this user profile and songs for consistent examples:

**User Profile:**
- favorite_genre: "pop"
- favorite_mood: "happy"
- target_energy: 0.85
- target_valence: 0.80
- target_danceability: 0.80
- target_acousticness: 0.15

**Songs:** Use the 10 songs from data/songs.csv

---

## Calculation Example (Full Walkthrough for Visualization)

**Song: "Sunrise City" by Neon Echo**
- Genre: pop | Mood: happy | Energy: 0.82 | Valence: 0.84 | Danceability: 0.79 | Acousticness: 0.18

**Step 1: Categorical Score**
- genre_match = 1.0 (pop == pop)
- mood_match = 1.0 (happy == happy)
- categorical_score = (1.0 + 1.0) / 2 = **1.0**

**Step 2: Numeric Features**
- energy_sim = 1 - |0.82 - 0.85| = 0.97
- valence_sim = 1 - |0.84 - 0.80| = 0.96
- danceability_sim = 1 - |0.79 - 0.80| = 0.99
- acousticness_sim = 1 - |0.18 - 0.15| = 0.97

**Step 3: Numeric Score**
- numeric_score = 0.30(0.97) + 0.25(0.96) + 0.25(0.99) + 0.20(0.97) = **0.977**

**Step 4: Final Score**
- SCORE = 0.40(1.0) + 0.60(0.977) = **0.986**

Visualize this as a stepped calculation with intermediate values highlighted.

---

## Ranking Example (for Visualization 7)

Given top 5 songs with scores: [0.986, 0.91, 0.88, 0.85, 0.82]

Apply variety penalties:
1. Order by score: [Song1(0.986), Song3(0.91), Song5(0.88), Song2(0.85), Song4(0.82)]
2. Check genre/mood consecutive patterns
3. Reorder to maximize variety_bonus total
4. Show before/after with penalties annotated

---

## Success Criteria

A complete visualization set should:
✓ Show mathematical formula hierarchy
✓ Demonstrate weight distribution impact
✓ Visualize feature similarity curves
✓ Display complete calculation flow
✓ Compare score-only vs. ranking results
✓ Include at least one interactive/sensitivity plot
✓ Use sample data from songs.csv consistently
✓ Label all components clearly

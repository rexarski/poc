+++
author = "rexarski"
title = "Emotion Trend Analysis in Video Transcripts"
date = "2025-01-08"
description = "Using embedding-based similarity to analyze emotional content in YouTube video transcripts and visualize emotion trends over time."
tags = [
    "machine-learning",
    "nlp",
    "embeddings",
    "emotion-analysis",
]
categories = [
    "experiments",
    "data-science",
]
+++

Can we quantitatively analyze emotional patterns in video transcripts using embedding similarity? This experiment uses text embeddings to identify dominant emotions and visualize trends across video segments.

<!--more-->

## Methodology

The approach uses **embedding-based similarity** to map transcript segments to emotion vectors. 

1. **Baseline Creation**: Compute average embeddings for six emotions (sadness, joy, love, anger, fear, surprise) from the `dair-ai/emotion` dataset using `embeddinggemma` via Ollama.

2. **Transcript Processing**: Load YouTube transcripts, group by video, and chunk long transcripts at sentence boundaries to comply with token limits.

3. **Emotion Analysis**: For each segment, calculate cosine similarity to each emotion baseline and identify the dominant emotion.

4. **Visualization**: Normalize scores per segment (deviation from mean) to highlight relative differences even when emotions co-vary.

```python
EMOTION_DATASET = "dair-ai/emotion"
EMOTIONS = ["sadness", "joy", "love", "anger", "fear", "surprise"]
```

## What We Did

We processed 100 YouTube video transcripts, generating embeddings for each segment and comparing them against emotion baselines. The system:

- Automatically handles transcript chunking at sentence boundaries
- Caches baseline embeddings for reuse
- Processes transcripts incrementally (skips already-computed segments)
- Generates normalized trend visualizations showing emotion deviations over time

Results include similarity scores for all six emotions per segment, with dominant emotion identification. Example output:

```csv
video_id,segment_id,dominant_emotion,sadness,joy,love,anger,fear,surprise
FdjVoOf9HN4,0,love,0.126,0.156,0.172,0.168,0.128,0.145
x1lAcT3xl5M,0,love,0.146,0.156,0.170,0.160,0.158,0.167
```

![Emotion Trend Analysis](/emotion-analysis-trends.png)

## What Can Be Achieved

This method enables **quantitative emotion analysis** at scale:

- **Pattern Discovery**: Identify emotion trends across video segments, revealing how emotional content evolves
- **Comparative Analysis**: Compare emotion profiles across different videos or video types
- **Temporal Insights**: Understand emotional arcs and transitions within video content
- **Automated Classification**: Categorize content by dominant emotions for organization and discovery

Future extensions could include computing emotion complexity (Shannon entropy), PCA/UMAP visualizations of emotional landscapes, and multi-video aggregation for broader insights.

## Does It Answer the Research Question?

**Yes**—the emotion trend analysis successfully provides the quantitative summary and visualization described in the objectives. It demonstrates:

✅ **Quantitative emotion similarity scores** across video segments  
✅ **Normalized visualizations** highlighting relative emotion differences  
✅ **Dominant emotion identification** per segment  
✅ **Temporal trends** showing how emotions evolve throughout videos

The normalization approach (deviation from segment mean) effectively reveals patterns even when absolute similarity scores are close, addressing the challenge of detecting relative emotion differences. This validates that embedding-based similarity can systematically analyze emotional content in spoken transcripts.

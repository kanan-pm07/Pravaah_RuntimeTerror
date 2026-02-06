project:
  title: "Causal Analysis and Interactive Reasoning over Conversational Data"
  description: >
    This project implements an end-to-end system for causal analysis and interactive
    reasoning over multi-turn conversational transcripts. The system goes beyond
    outcome prediction by identifying why an outcome occurred using faithful,
    evidence-backed dialogue turns and supports multi-turn analytical queries.

objectives:
  - Predict outcome events such as refunds, escalations, delays, and resolutions
  - Identify causal dialogue turns responsible for each outcome
  - Provide interpretable and traceable explanations
  - Support interactive follow-up queries with contextual consistency
  - Avoid hallucination through model-driven causal attribution

system_architecture:
  stages:
    - stage: "Stage 1"
      name: "Outcome Prediction"
      description:
        - Transformer-based (BERT) conversation classifier
        - Predicts the final outcome of a conversation
    - stage: "Stage 2"
      name: "Turn-Level Causal Attribution"
      description:
        - Leave-One-Out (LOO) confidence drop analysis
        - Assigns importance scores to dialogue turns
        - Extracts top-ranked turns as causal evidence
    - stage: "Stage 3"
      name: "Interactive Query Handling"
      description:
        - Handles natural-language analytical queries
        - Maintains context across multiple turns
        - Returns structured explanations with evidence

project_structure:
  files_and_directories:
    - structured_dataset.csv
    - queries.csv
    - results/
    - logs/
    - notebook.ipynb
    - requirements.txt
    - README.md

dataset:
  description: >
    The dataset consists of structured conversational transcripts. Each conversation
    contains multiple dialogue turns, while the outcome label is defined at the
    conversation level.
  columns:
    - transcript_id: "Unique identifier for each conversation"
    - turn_id: "Sequential order of dialogue turns"
    - speaker: "Speaker role (Agent or Customer)"
    - text: "Utterance content"
    - intent: "High-level issue category (e.g., delivery, appointment)"
    - domain: "Business domain"
    - reason: "Outcome explanation label"
  preprocessing_notes:
    - Only spoken dialogue turns (Agent and Customer) are used
    - System summaries and metadata entries are excluded to prevent label leakage

setup:
  environment:
    python_version: "Python 3.9 or higher"
    virtual_environment:
      create: "python -m venv venv"
      activate_linux_mac: "source venv/bin/activate"
      activate_windows: "venv\\Scripts\\activate"
  installation:
    command: "pip install -r requirements.txt"

execution:
  stage_1:
    name: "Outcome Prediction Training"
    steps:
      - Open the provided notebook
      - Run all cells under Stage 1
      - Train the BERT-based classifier
      - Best model checkpoint is saved automatically in the results directory
  stage_2:
    name: "Turn-Level Evidence Extraction"
    steps:
      - Load the trained model
      - Apply leave-one-out attribution on dialogue turns
      - Rank dialogue turns by causal importance
    example_output:
      importance: 0.79
      turn: "Customer: The tracking shows delivered, but nothing arrived."
  stage_3:
    name: "Query-Driven Interaction"
    example_queries:
      - "Why do delivery-related conversations result in refunds?"
      - "Which dialogue turn contributed most to the outcome?"
    behavior:
      - Filters relevant conversations
      - Extracts causal evidence
      - Maintains context for follow-up queries

query_csv:
  file: "queries.csv"
  contents:
    - Query ID
    - Query text
    - Query category
    - System output
    - Remarks explaining causal reasoning

evaluation:
  metrics:
    - Accuracy
    - Macro F1-score
    - Evidence faithfulness
    - Turn-level ID recall
  stage_1_results:
    accuracy: 1.0
    macro_f1_score: 1.0

faithfulness:
  guarantee:
    - Model-driven leave-one-out causal attribution
    - Confidence-drop based importance scoring
    - Exact dialogue turns extracted as evidence
    - No generative hallucination used

reproducibility:
  steps:
    - Use the provided dataset
    - Run notebook cells sequentially
    - Maintain the same random seed and environment
    - Use the provided requirements.txt file

future_work:
  - Hierarchical turn-level Transformer models
  - Temporal modeling using timestamps
  - Visualization dashboards for causal evidence
  - Cross-conversation causal pattern mining

conclusion: >
  This project demonstrates how conversational machine learning systems can move
  beyond prediction toward causal, interpretable, and interactive reasoning.
  The proposed approach is scalable, faithful, and well-aligned with real-world
  conversational analytics requirements.

contact:
  note: "Refer to the technical report or notebook documentation for additional details."

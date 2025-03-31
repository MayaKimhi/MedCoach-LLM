# MedCoach: LLM-Powered Clinical Reasoning Trainer

MedCoach is an AI-powered learning tool that helps medical students sharpen their diagnostic skills through interactive clinical case simulations. 
The system generates realistic patient scenarios and evaluates student responses, providing immediate feedback and corrections.

## Our Motivation

Medical students often rely on static teaching methods that lack the complexity and variability of real-world clinical scenarios. MedCoach offers an interactive, case-based learning experience that promotes diagnostic reasoning, clinical decision-making, and immediate feedback.

## Key Features

- **LLM-based clinical case generation** from real medical QA datasets
- **Student input**: free-text diagnosis per case
- **Student Answer classification**: correct/incorrect
- **Feedback and correct answer suggestions**

## The Dataset

We use [MedQuad dataset](https://www.kaggle.com/datasets/thedevastator/comprehensive-medical-q-a-dataset?resource=download), which contains over 16,000 real-life medical questions and expert answers.

| Column | Description |
|--------|-------------|
| `Question Type` | Type of medical question | String |
| `Question` | Patient question | String |
| `Answer` | Expert response | String |

In addition, synthetic data is generated using LLM to expand coverage and create rich clinical scenarios.

# Created by Maya Kimhi & Mai Werthaim as part of the “Introduction to Natural Language Processing” course

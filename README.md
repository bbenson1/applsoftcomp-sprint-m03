# AI Job Search Agent

An AI-assisted job search agent built in OpenCode as part of a context-engineering sprint. The agent is designed to match roles to user preferences, store feedback across sessions, and improve future recommendations through a structured multi-agent workflow.

## Project Overview

This project explores how AI agents can support a high-volume job search by combining user preference memory, feedback loops, and task-specific sub-agents. The goal was to turn broad job-search criteria into more relevant, actionable recommendations over time.

## How It Works

- Collects user role preferences at the start of a session
- Stores preferences and feedback in local files for persistence across sessions
- Uses specialized sub-agents for job retrieval, feedback collection, and preference learning
- Captures favorite and least-favorite job feedback to update future recommendations
- Produces structured job results with relevant fields and clickable links

## Status

Prototype / agent workflow. This project demonstrates the design of a personalized AI job-search assistant using memory, feedback, and sub-agent task decomposition. It is not presented as a production-scale job scraping platform.



# Assignment:

# Build a Personalized Assistant

> [!IMPORTANT]
> **Fork this repo first.** If you skip this step, your Codespace will open on the original repo and you will have no way to save or push your work. Your changes will be lost when the Codespace is deleted.
>
> Fork: click **Fork** (top-right of this page) and create a copy under your own account. Then follow the steps below from your fork.

Build a personalized AI assistant from scratch. You will practice the three core primitives of context engineering—**write**, **select**, and **isolate**—by designing an agent that learns your preferences and improves over time.

We use [opencode](https://opencode.ai/) as the coding environment. `claude code` users: rename `.agents` to `.claude`.

## Steps

1. [Before you start](docs/before-you-start.md)
2. [Launch the codespaces](docs/codespaces.md)
3. [Setup](docs/setup.md) - connect your API key and install dependencies
4. [Demo](docs/demo.md) - run the example skills to understand the patterns
5. [Your Task](docs/task.md) - build your own skill


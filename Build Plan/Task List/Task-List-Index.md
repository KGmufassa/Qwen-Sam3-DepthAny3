# Task List Index

## Purpose

This folder contains the concrete implementation task lists for each vertical slice.

The tasks assume the locked implementation stack:

- frontend: Next.js + React + TypeScript + PixiJS
- control plane: separate backend service
- database: PostgreSQL
- queue: Redis-backed queue
- storage: MinIO locally with S3-compatible abstraction
- workers: Python
- hosting: hybrid local-first with remote GPU workers when needed
- repo: monorepo/workspace with separate apps and services

---

## Slice Task Lists

- [Slice-1-Task-List.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Task%20List/Slice-1-Task-List.md)
- [Slice-2-Task-List.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Task%20List/Slice-2-Task-List.md)
- [Slice-3-Task-List.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Task%20List/Slice-3-Task-List.md)
- [Slice-4-Task-List.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Task%20List/Slice-4-Task-List.md)
- [Slice-5-Task-List.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Task%20List/Slice-5-Task-List.md)
- [Slice-6-Task-List.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Task%20List/Slice-6-Task-List.md)
- [Slice-7-Task-List.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Task%20List/Slice-7-Task-List.md)
- [Slice-8-Task-List.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Task%20List/Slice-8-Task-List.md)
- [Slice-9-Task-List.md](/Users/wislemleger/Desktop/GitHub/Qwen-Sam3-DepthAny3/Build%20Plan/Task%20List/Slice-9-Task-List.md)

---

## Task Structure

Each slice task list is grouped into:

- workspace and shared contracts
- frontend tasks
- control-plane tasks
- worker tasks
- infrastructure tasks
- QA and verification tasks

---

## Execution Rule

Tasks should be executed in slice order unless a task is clearly marked as parallelizable and does not violate earlier frozen contracts.

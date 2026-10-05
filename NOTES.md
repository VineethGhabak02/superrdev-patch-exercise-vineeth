# Patch Exercise Notes

## Summary

I fixed four focused issues across the backend, database query layer, and frontend.

1. Added validation for `page` and `pageSize` so invalid pagination returns HTTP 400 instead of causing a server error.
2. Fixed search query operator precedence so archived tasks are excluded and the status filter applies to both title and description matches.
3. Fixed the React task-loading state so failed requests clear the loading state and stale errors are cleared when a new request starts.
4. Reset pagination to page 1 when the search query or status filter changes.

## What I did not change

I did not rewrite the application architecture, change the API contract, or modify unrelated components. `api.js`, `SearchBar`, `StatusFilter`, and `TaskTable` were left unchanged because they were functioning correctly for the exercised flows.

## Biggest remaining risk

The search implementation currently loads matching records before performing pagination in Java. This could become inefficient as the task dataset grows. A database-level paginated query would scale better, but changing that was outside this focused patch.

## AI/tools used

I used ChatGPT to assist with code inspection, identifying likely defects, suggesting focused fixes, and designing verification tests. I reviewed the suggested changes, applied them manually, and verified the behavior using the running Spring Boot API and React application.

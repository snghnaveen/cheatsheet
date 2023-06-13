---
sidebar_position: 1
---

# Frequently used git commands

1. Empty commit : 
    ```bash
    git commit --allow-empty -m "trigger"
    ```
1. Reset uncommitted changes : 
    ```bash
    git reset --hard HEAD
    ```
1. Reset last commit : 
    ```bash
    git reset --hard HEAD~1
    ```
1. Reset single file : 
    ```bash
    git checkout master -- filename
    ```

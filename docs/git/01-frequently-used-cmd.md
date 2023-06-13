---
sidebar_position: 1
---

# Frequently used git commands

1. Empty commit : 
    ```
    git commit --allow-empty -m "trigger"
    ```
1. Reset uncommitted changes : 
    ```
    git reset --hard HEAD
    ```
1. Reset last commit : 
    ```
    git reset --hard HEAD~1
    ```
1. Reset single file : 
    ```
    git checkout master -- filename
    ```

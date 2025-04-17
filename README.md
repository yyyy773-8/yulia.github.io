name: post_pr

on:
    push:
        branches:
            - 'main'
    workflow_dispatch:

jobs:
    build:
        runs-on: ubuntu-latest
        steps:
            - uses: actions/checkout@v3

            - run: mkdir -p protocol/cargo-cache
            - run: mkdir -p protocol/target
            - run: mkdir -p node_modules
            - run: mkdir -p ~/.cache/Cypress

            # build the code here!

            - name: Save cache
              uses: actions/cache/save@v3
              if: always()
              with:
                  path: |
                      protocol/cargo-cache
                      protocol/target
                      node_modules
                      ~/.cache/Cypress
                  key: project-cache-${{ runner.os }}-${{ runner.arch }}

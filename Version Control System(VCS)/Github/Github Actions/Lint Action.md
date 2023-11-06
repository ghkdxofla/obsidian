# Abstract
- **Shows linting errors** on GitHub commits and PRs
- Allows **auto-fixing** issues
- Supports [many linters and formatters](https://github.com/marketplace/actions/lint-action#supported-tools)
# Setup
- `./github/workflows/lint.yml` 등에 아래의 workflow를 추가한다
```yaml
name: Lint

on:
  # Trigger the workflow on push or pull request,
  # but only for the main branch
  push:
    branches:
      - main
  # Replace pull_request with pull_request_target if you
  # plan to use this action with forks, see the Limitations section
  pull_request:
    branches:
      - main

# Down scope as necessary via https://docs.github.com/en/actions/security-guides/automatic-token-authentication#modifying-the-permissions-for-the-github_token
permissions:
  checks: write
  contents: write

jobs:
  run-linters:
    name: Run linters
    runs-on: ubuntu-latest

    steps:
      - name: Check out Git repository
        uses: actions/checkout@v3

      # Install your linters here

      - name: Run linters
        uses: wearerequired/lint-action@v2
        with:
          # Enable your linters here
```
### [[Javascript & Typescript]] 적용 시
- [[Lint]] 와 [[Prettier]] 설정을 repository에 먼저 적용한다
```yaml
name: Lint

on:
  # Trigger the workflow on push or pull request,
  # but only for the main branch
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  run-linters:
    name: Run linters
    runs-on: ubuntu-latest

    steps:
      - name: Check out Git repository
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v1
        with:
          node-version: 12

      # ESLint and Prettier must be in `package.json`
      - name: Install Node.js dependencies
        run: npm ci

      - name: Run linters
        uses: wearerequired/lint-action@v2
        with:
          eslint: true
          prettier: true
```
### [[Python]] 적용 시
- Flake8과 Black 설정을 Repository에 먼저 적용한다
```yaml
name: Lint

on:
  # Trigger the workflow on push or pull request,
  # but only for the main branch
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  run-linters:
    name: Run linters
    runs-on: ubuntu-latest

    steps:
      - name: Check out Git repository
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v1
        with:
          python-version: 3.8

      - name: Install Python dependencies
        run: pip install black flake8

      - name: Run linters
        uses: wearerequired/lint-action@v2
        with:
          black: true
          flake8: true
```
# Reference
- [Lint Action](https://github.com/marketplace/actions/lint-action)
- [CICD-Github-Actions로-CI-세팅하기Prettier-ESLint-TSC](https://velog.io/@sjoleee_/CICD-Github-Actions%EB%A1%9C-CI-%EC%84%B8%ED%8C%85%ED%95%98%EA%B8%B0Prettier-ESLint-TSC)
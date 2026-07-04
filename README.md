# ADF CI/CD Pipeline Project

This repository manages the CI/CD lifecycle for Azure Data Factory (ADF) projects, ensuring a robust, automated deployment strategy from development to production using Azure DevOps.

## Overview
This project bridges the gap between local development and cloud-based orchestration. It utilizes **Azure DevOps** to automate the lifecycle of data pipelines, ensuring that code changes are consistently validated, tested, and deployed across different environments.

## Environment Strategy
We utilize a three-tier environment strategy to ensure stability and data integrity:

* **DEV (Development)**: The primary environment where developers build and test new pipelines. Changes are integrated and validated here first.
* **QA (Quality Assurance)**: The staging environment that mirrors production configurations. This stage is used for User Acceptance Testing (UAT) and verifying pipeline performance with realistic data.
* **PD (Production)**: The live environment. Deployments to this environment are strictly controlled, requiring successful validation in QA and formal approval gates within Azure DevOps.

## Pipeline Workflow
The deployment process is automated through Azure DevOps pipelines:

1. **CI (Continuous Integration)**: Triggered upon code changes, the `ci_build.yml` pipeline validates ARM templates and generates build artifacts.
2. **CD (Continuous Deployment)**: The `cd_deploy.yml` pipeline manages environment-specific deployments.
    * Parameters are dynamically injected using environment-specific files located in `cicd/ARMParams/` (`dev.json`, `qa.json`, `pd.json`).
    * Deployment to the **PD** environment is configured with strict manual approval requirements to ensure security and stability.

## Getting Started
* **Git Configuration**: Ensure your local development environment is synced with this repository. Note that the `factory/` directory and sensitive local configs are excluded via `.gitignore` to maintain a clean and secure repository.
* **Deployment**: Always verify the corresponding ARM parameter file in `cicd/ARMParams/` before triggering a deployment to the **PD** environment.
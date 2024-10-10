
# Jenkins Pipeline for Multi-Language Build and Execution

## Pipeline Overview

This Jenkins pipeline allows you to build and run code in multiple languages (C, Python, and Bash). The language can be selected using pipeline parameters, or all languages can be processed by default.

## Parameters

- **Language**: A choice parameter with the following options:
  - `All`: Run the pipeline stages for all languages.
  - `C`: Build and run only the C program.
  - `Python`: Run only the Python program.
  - `Bash`: Run only the Bash script.

  The default selection is `All`.

## Environment

- **LOG_DIR**: A directory to store log files, located at `${WORKSPACE}/logs`.

## Stages

### 1. **Initialize**
- **Purpose**: Sets up the log directory (`${LOG_DIR}`) to store logs generated during the pipeline execution.
- **Steps**:
  - Creates the `logs` directory if it doesn’t already exist.

### 2. **Build C**
- **Condition**: Runs when the `Language` parameter is either `All` or `C`.
- **Purpose**: Compiles a C program (`hello.c`) and redirects the compiler output to a log file.
- **Steps**:
  - Ensures the `logs` directory exists.
  - Compiles `hello.c` using `gcc` and writes the output to `c_compile.log`.

### 3. **Run C**
- **Condition**: Runs when the `Language` parameter is either `All` or `C`.
- **Purpose**: Executes the compiled C program and logs the output.
- **Steps**:
  - Ensures the `logs` directory exists.
  - Runs the compiled C program (`./hello`) and writes the output to `c_output.log`.

### 4. **Run Python**
- **Condition**: Runs when the `Language` parameter is either `All` or `Python`.
- **Purpose**: Executes the Python program (`hello.py`) and logs the output.
- **Steps**:
  - Ensures the `logs` directory exists.
  - Runs the Python script and writes the output to `python_output.log`.

### 5. **Run Bash**
- **Condition**: Runs when the `Language` parameter is either `All` or `Bash`.
- **Purpose**: Executes the Bash script (`hello.sh`) and logs the output.
- **Steps**:
  - Ensures the `logs` directory exists.
  - Runs the Bash script and writes the output to `bash_output.log`.

## Post Actions

- **Always**: Archives the log files generated during the pipeline stages (`logs/*.log`), allowing empty archives if no logs were created.
- **Notification**: Displays a message confirming that the logs have been archived.

## How to Run the Pipeline

1. **Trigger the Pipeline**: You can trigger the pipeline from Jenkins and choose the desired language (`All`, `C`, `Python`, or `Bash`) via the parameter input.
2. **Log Files**: The logs for each language will be stored in the `${WORKSPACE}/logs` directory. Each stage will create its own log file:
   - `c_compile.log` for the C compilation output.
   - `c_output.log` for the C program execution output.
   - `python_output.log` for the Python program output.
   - `bash_output.log` for the Bash script output.

3. **Post-build Actions**: Once the pipeline is complete, all log files are archived for future reference.

## Notes

- Make sure the source files (`hello.c`, `hello.py`, `hello.sh`) exist in the workspace before running the pipeline.
- If there are any errors during compilation or execution, they will be captured in the respective log files.

---

This pipeline demonstrates the use of Jenkins for orchestrating multi-language builds and executions, making it flexible for different programming environments.

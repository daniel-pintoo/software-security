# Python Web Vulnerability Analyzer

Static analysis tool for detecting insecure information flows in Python web application slices.

This project was developed for the Software Security course at Instituto Superior Tecnico. It performs taint-style analysis over Python ASTs to identify flows from untrusted sources to sensitive sinks while tracking sanitization and implicit flows.

## Overview

The analyzer receives:

- a Python slice to inspect
- a JSON file describing vulnerability patterns

It parses the input slice into a Python AST, propagates labels through expressions and statements, and emits a structured JSON report describing potential vulnerabilities.

## What The Tool Detects

The tool supports configurable vulnerability definitions with:

- sources
- sanitizers
- sinks
- implicit-flow handling

The included `5_patterns.json` file defines example patterns for:

- XSS
- SQL injection
- command injection
- path traversal
- SSRF

## Main Features

- AST-based static analysis of Python code slices
- explicit and implicit information-flow tracking
- sanitizer-aware reporting
- configurable vulnerability patterns via JSON
- deterministic JSON output for detected flows

## Repository Contents

- `py_analyzer.py` - main analyzer implementation
- `5_patterns.json` - sample vulnerability patterns used by the analyzer

## Usage

Run the analyzer with:

```sh
python py_analyzer.py <path_to_slice.py> <path_to_patterns.json>
```

Example:

```sh
python py_analyzer.py slices/example.py 5_patterns.json
```

The tool writes the result to:

```text
output/<slice>.output.json
```

## Analysis Approach

The implementation models:

- source introduction from configured names and uninitialized variables
- propagation through names, attributes, subscripts, calls, assignments, conditionals, and loops
- sanitizer application on matching function calls
- sink detection on both function calls and assignments
- implicit control-flow influence through program-counter tracking

## Why This Project Matters

This project demonstrates:

- practical static program analysis
- reasoning about taint propagation and sanitization
- secure software concepts applied to Python web vulnerabilities
- translating a formal-ish security specification into working code

## Possible Improvements

- broader Python language coverage
- richer test corpus and benchmark suite
- improved precision to reduce false positives
- support for larger real-world codebases beyond isolated slices

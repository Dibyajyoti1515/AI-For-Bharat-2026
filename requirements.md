# Requirements Document

## Introduction

CodeDrishti is an AI-powered tool designed for the AI FOR BHARAT 2026 hackathon to help developers understand unfamiliar codebases faster. The system enables students, junior developers, and engineers onboarding to new projects to quickly comprehend code structure and functionality through automated analysis and natural language explanations.

## Glossary

- **CodeDrishti**: The AI-powered codebase understanding system that provides automated analysis and natural language explanations
- **Repository**: A code repository from GitHub or local filesystem containing source code files
- **Entry_Point**: Main files that serve as starting points for understanding a codebase (e.g., main.py, index.js, App.tsx)
- **File_Explanation**: AI-generated natural language description of what a code file does and its role in the system
- **Semantic_Search**: Intent-based search that finds code based on functionality rather than exact text matches
- **Ingestion_Engine**: Component responsible for loading and processing repository files while respecting ignore patterns
- **Analysis_Engine**: Component that identifies entry points and generates explanations for code files
- **Search_Engine**: Component that performs semantic code search using natural language queries
- **3D_Graph**: Interactive three-dimensional visualization of codebase architecture and file dependencies
- **RAG_Search**: Retrieval-Augmented Generation search against official documentation knowledge bases
- **Bharat_Mode**: Localized explanation mode using Indian analogies and multi-lingual support for accessibility

## Requirements

### Requirement 1: Repository Ingestion

**User Story:** As a developer, I want to load a codebase from GitHub or local filesystem, so that I can analyze any project structure.

#### Acceptance Criteria

1. WHEN a user provides a GitHub repository URL, THE Ingestion_Engine SHALL clone and load all source files
2. WHEN using CLI in a local directory, THE Ingestion_Engine SHALL scan the filesystem recursively
3. WHILE ingesting, THE Ingestion_Engine SHALL ignore files matching .gitignore patterns and common dependency folders (node_modules, .git, __pycache__)
4. WHEN ingestion completes, THE Ingestion_Engine SHALL output a structural summary containing file count and directory structure
5. IF a private repository is detected, THEN THE Ingestion_Engine SHALL prompt for authentication credentials

### Requirement 2: Entry Point Detection

**User Story:** As a developer new to a codebase, I want to identify the main entry points, so that I know where to start reading the code.

#### Acceptance Criteria

1. WHILE analyzing a codebase, THE Analysis_Engine SHALL identify common entry point patterns for each supported programming language (Python, JavaScript, Java, C++, Go)
2. WHEN analyzing a repository, THE Analysis_Engine SHALL rank entry points by likelihood score from 0.0 to 1.0 of being the main starting point
3. WHEN multiple entry points exist, THE Analysis_Engine SHALL categorize them by type (application, test, build, configuration)
4. THE Analysis_Engine SHALL detect package.json scripts, Makefile targets, and other build configuration entry points
5. WHEN no clear entry points are found, THE Analysis_Engine SHALL suggest the three most likely candidates based on file structure and import patterns

### Requirement 3: AI-Based File Explanation

**User Story:** As a developer, I want to understand what each file does without reading all the code, so that I can quickly grasp the codebase structure.

#### Acceptance Criteria

1. WHEN a user selects a file, THE Analysis_Engine SHALL generate a natural language explanation of the file's purpose and functionality
2. WHEN a file is selected for explanation, THE Analysis_Engine SHALL identify key functions, classes, and their relationships within each file
3. THE Analysis_Engine SHALL highlight important dependencies and describe how the file fits into the overall architecture
4. WHEN explaining a file, THE Analysis_Engine SHALL use appropriate technical terminology while maintaining readability for junior developers
5. THE Analysis_Engine SHALL generate explanations within 15 seconds for files containing up to 500 lines of code

### Requirement 4: 3D Architectural Visualization

**User Story:** As a developer, I want to see a 3D visual map of the codebase, so that I can understand the system architecture and dependencies at a glance.

#### Acceptance Criteria

1. THE Analysis_Engine SHALL generate a node-link JSON structure representing file dependencies and folder hierarchy
2. WHEN the ingestion is complete, THE CodeDrishti SHALL render an interactive 3D Force-Directed Graph in the web interface
3. WHEN a user clicks a node in the 3D view, THE CodeDrishti SHALL highlight all connected dependencies
4. THE CodeDrishti SHALL use distinct color-coding to distinguish between Entry Points (red), Utilities (blue), and Infrastructure files (green)
5. THE Analysis_Engine SHALL generate a system-level dependency graph showing interaction patterns between different entry points across the repository

### Requirement 5: Contextual Documentation Explainer

**User Story:** As a developer, I want my code explained using official technical documentation, so that I can understand the underlying technology while looking at my specific implementation.

#### Acceptance Criteria

1. THE Analysis_Engine SHALL perform RAG search against official documentation stored in knowledge bases
2. WHEN explaining a code block, THE CodeDrishti SHALL provide documentation references and snippets
3. THE CodeDrishti SHALL link code patterns to their corresponding documentation examples
4. WHEN multiple documentation sources exist, THE Analysis_Engine SHALL prioritize official sources over community content
5. THE CodeDrishti SHALL provide contextual explanations that connect the specific code to broader architectural patterns
6. WHILE performing a RAG search, THE system SHALL utilize Amazon Bedrock Knowledge Bases to ensure high-speed retrieval of indexed documentation.
7. IF a query is made in a regional Indian language, THE system SHALL use Amazon Translate to provide a localized technical response.

### Requirement 6: Semantic Code Search

**User Story:** As a developer, I want to search for code using natural language descriptions, so that I can find functionality without knowing exact function names.

#### Acceptance Criteria

1. WHEN a user enters a natural language query, THE Search_Engine SHALL return relevant code files and functions
2. THE Search_Engine SHALL understand intent-based queries like "authentication logic" or "database connection setup"
3. WHEN displaying search results, THE Search_Engine SHALL show code snippets with explanations of why they match the query
4. THE Search_Engine SHALL rank results by relevance score from 0.0 to 1.0 and provide confidence scores for each match
5. WHEN no exact matches are found, THE Search_Engine SHALL suggest up to three related functionality options or alternative search terms

### Requirement 7: Bharat Contextual Bridge

**User Story:** As an Indian engineering student, I want to see complex concepts explained using local analogies, so that I can understand abstract technology through familiar examples.

#### Acceptance Criteria

1. WHEN the "Bharat Mode" is toggled, THE Analysis_Engine SHALL generate analogies based on Indian infrastructure (e.g., explaining Kafka using the Indian Railways or Dabbawala system)
2. WHEN requested, THE Analysis_Engine SHALL provide multi-lingual summaries in Hindi, Odia, Tamil, or other major Indian languages to assist students from non-English backgrounds
3. THE Analysis_Engine SHALL use familiar Indian examples like cricket team structures, railway systems, or local governance hierarchies to explain software architecture patterns
4. WHEN explaining distributed systems, THE Analysis_Engine SHALL draw parallels to Indian logistics networks like postal services, supply chains, or delivery systems
5. THE CodeDrishti SHALL maintain technical accuracy while making complex concepts accessible through relevant cultural context

### Requirement 8: Privacy and Security

**User Story:** As a developer working with proprietary code, I want assurance that my code is handled securely, so that I can use CodeDrishti with confidence.

#### Acceptance Criteria

1. THE CodeDrishti SHALL process code locally when possible to minimize data transmission
2. WHEN using external AI services, THE CodeDrishti SHALL only send necessary code snippets, not entire repositories
3. THE CodeDrishti SHALL provide clear disclosure information about what data is transmitted to external AI services
4. THE CodeDrishti SHALL validate and sanitize all user inputs to prevent injection attacks and security vulnerabilities
5. WHERE user consent is explicitly provided, THE CodeDrishti SHALL store analysis results locally for improved performance on subsequent runs
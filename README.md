# HW06 – API Testing Report & Deliverables

## Student & Submission Information

| Information | Details |
| --- | --- |
| **Student Name** | HỒ GIA HUY |
| **Student ID** | 23127376 |
| **Class / Group** | 23KTPM2 / 23CLC |
| **Self-Assessed Grade** | [Chưa đánh giá] |
| **Public GitHub Repo** | [Link GitHub Repository] |
| **Video Skill Demo Link** | [Link Video Demo YouTube] |

---

## 1. Assessment & Self-Evaluation Table

| No. | Criteria | Max Grade | Self-Assessed Grade | Notes / Highlights |
| --- | --- | --- | --- | --- |
| **1** | **API 1 (Pool A - Auth/Product)** — full pipeline (generate + audit + extend + execute + bugs) | 30 | [TBD] | Selected API: [TBD] |
| **2** | **API 2 (Pool B - Cart/Order)** — full pipeline (generate + audit + extend + execute + bugs) | 30 | [TBD] | Selected API: [TBD] |
| **3** | **API 3 (Pool C - Admin)** — full pipeline (generate + audit + extend + execute + bugs) | 30 | [TBD] | Selected API: [TBD] |
| **4** | **Agent Skills** (AI-driven test generator design, diagram, pseudocode) | 10 | [TBD] | [TBD] |
| **TOTAL** | | **100** | **[TBD]** | |

---

## 2. Test Summary Report

| Metric | API 1 (Pool A) | API 2 (Pool B) | API 3 (Pool C) | Total |
| --- | --- | --- | --- | --- |
| **Selected API Endpoint** | `[TBD]` | `[TBD]` | `[TBD]` | 3 APIs |
| **AI Generated Cases** | [TBD] | [TBD] | [TBD] | [TBD] |
| **Audited Cases (Valid)** | [TBD] | [TBD] | [TBD] | [TBD] |
| **Human Extended Cases** | [TBD] | [TBD] | [TBD] | [TBD] |
| **Total Test Cases Executed** | [TBD] | [TBD] | [TBD] | [TBD] |
| **Passed Cases** | [TBD] | [TBD] | [TBD] | [TBD] |
| **Failed Cases** | [TBD] | [TBD] | [TBD] | [TBD] |
| **Bugs Found & Logged** | [TBD] | [TBD] | [TBD] | [TBD] |

---

## 3. Submission Directory Structure

```text
<StudentID>_HW06_AI_API_<SelfAssessedGrade>/
├── README.md                                # Self-assessment table, test summary, project overview
├── git_commit_log.txt                       # Git commit history log (text file)
│
├── reports/                                 # Documentation & Technical Reports
│   ├── main_report.md                       # Main API Testing Report (Pipeline, audit, bugs, features)
│   └── cicd_report.md                       # CI/CD Pipeline Report (configuration, runs, screenshots)
│
├── postman/                                 # Postman Test Suites & Execution Artifacts
│   ├── collections/                         # Postman collection files (.json)
│   │   └── SUT_API_Testing.postman_collection.json
│   ├── environments/                        # Postman environment configuration files (.json)
│   │   └── EShop_Local.postman_environment.json
│   ├── data/                                # Data-driven test files (JSON / CSV)
│   │   └── test_data.json
│   └── newman/                              # Newman HTML execution reports
│       ├── report_pass.html                 # 100% Passing run report
│       └── report_fail.html                 # Failed assertion test run report
│
├── test_cases/                              # Test Cases Deliverables
│   ├── HW06_TestCases_Summary.xlsx          # Excel test case matrix (AI generated, audited, extended)
│   └── test_cases_details.md                # Markdown detailed test specification
│
├── agent_skill/                             # G9.5 Agent Skill: AI API Test Generator
│   ├── diagram.mermaid                      # Architecture diagram source (Mermaid)
│   ├── diagram.png                          # Rendered self-drawn architecture diagram
│   └── SKILL.md                             # Agent Skill instructions (.md) for step-by-step test generation
│
├── video/                                   # Demonstration Video
│   └── video_demo_link.txt                  # Link to YouTube Demonstration Video
│
├── docs/                                    # SUT Original Documentation
│   ├── api_specification.md                 # Original SUT API markdown specification
│   └── eshop-sut.md                         # SUT requirements & architecture overview
│
├── api_spec/                                # OpenAPI Specifications
│   └── openapi_spec.yaml                    # Converted OpenAPI 3.0 specification
│
├── bugs/                                    # SUT Bug Reports & Evidence
│   ├── bug_reports.md                       # Detailed bug list & descriptions
│   └── screenshots/                         # Screenshots of bugs logged on GitHub Issues
│       ├── BUG-01_idor.png
│       └── BUG-02_state.png
│
├── ai_audit/                                # AI Compliance & Governance
│   ├── ai_audit_report.md                   # Complete AI Audit Log (Prompts, models, responses, dates)
│   └── ai_critique.md                       # AI Critique (200–300 words paragraph)
│
└── .github/                                 # CI/CD Workflow Configuration
    └── workflows/
        └── api_tests.yml                    # GitHub Actions workflow for Newman execution
```

---

## 4. Postman Features Exercised

- **Workspaces & Collections**: Structured test suite organization.
- **Environment & Collection Variables**: Dynamic token management and base URL configuration.
- **Pre-request Scripts**: Injection of mandatory `X-Student-Id: {StudentID}` header across all requests.
- **Test Scripts & Assertions**: Status code verification, JSON schema validation, latency checks.
- **Collection Runner & Data-Driven Testing**: Iterative test execution using external JSON/CSV dataset (`postman/data/test_data.json`).
- **Newman CLI Integration**: Automated local and CI/CD test execution producing HTML reports.

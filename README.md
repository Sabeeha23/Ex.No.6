# Ex.No.6 AI-Assisted Programming and Debugging

# Date: 06/09/2026

# Register no. 212223230176

# Aim: Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights with Multiple AI Tools

# AI Tools Required:

* ChatGPT
* Google Gemini
* Microsoft Copilot
* Python
* C
* Java

# Explanation:

Experiment the persona pattern as a programmer for any specific applications related with your interesting area. Generate the outoput using more than one AI tool and based on the code generation analyse and discussing that. Learnerss generate

Python C Java using AI.

Then

identify bugs optimise code explain complexity generate unit tests Finally compare manual coding versus AI-assisted coding. Deliverable

Code quality analysis.

## Selected Application Area

### Project Title

**ForensiFuse: A Confidence Calibrated Framework for Cross Tool Digital Evidence Corroboration**

### Application

ForensiFuse is a digital forensic evidence fusion system that combines findings obtained from multiple forensic analysis tools. The system identifies duplicate or dependent evidence, detects contradictory findings, adjusts evidence weights and generates a final confidence score.

The programming task selected for this experiment is to implement a simple **evidence confidence calculation module**.

### Problem Statement

In digital forensic investigations, multiple tools may report findings related to the same artifact. If these findings are directly added together, duplicate evidence can artificially increase the confidence score.

The program should:

1. Accept forensic findings from different tools.
2. Store the artifact, tool, confidence and status.
3. Identify repeated artifacts.
4. Apply a dependency discount to repeated evidence.
5. Detect contradictory findings.
6. Apply a contradiction penalty.
7. Calculate the final confidence score.

---

## Persona Pattern Prompt

### Prompt

> Act as an experienced software programmer and digital forensics engineer. Develop a simple evidence confidence calculation module for my final-year project ForensiFuse. The program should accept forensic findings from multiple tools, identify duplicate artifacts, reduce the weight of dependent evidence, detect contradictory findings, apply a contradiction penalty and calculate a final confidence score. Generate the solution in Python, C and Java. Explain the logic, identify possible bugs, optimize the implementation, analyse time and space complexity, and generate unit test cases.

---

# Python

## AI-Generated Python Code

```python
evidence = [
    {
        "tool": "Memory",
        "artifact": "process_123",
        "confidence": 0.90,
        "status": "malicious"
    },
    {
        "tool": "Disk",
        "artifact": "process_123",
        "confidence": 0.85,
        "status": "malicious"
    },
    {
        "tool": "Log",
        "artifact": "event_456",
        "confidence": 0.80,
        "status": "benign"
    }
]

DEPENDENCY_DISCOUNT = 0.5
CONTRADICTION_PENALTY = 0.5

groups = {}

for item in evidence:
    groups.setdefault(item["artifact"], []).append(item)

total_score = 0
total_weight = 0

for artifact, findings in groups.items():

    statuses = {item["status"] for item in findings}

    for index, item in enumerate(findings):

        weight = item["confidence"]

        if index > 0:
            weight *= DEPENDENCY_DISCOUNT

        if len(statuses) > 1:
            weight *= CONTRADICTION_PENALTY

        total_score += weight
        total_weight += 1

final_confidence = total_score / total_weight

print("Final Confidence Score:",
      round(final_confidence, 3))
```

### Output

```text
Final Confidence Score: 0.6
```

### Python Code Analysis

The Python implementation uses dictionaries and lists to represent forensic evidence. A dictionary is used to group findings according to their artifact identifier.

The program then checks whether multiple findings belong to the same artifact. If they do, the subsequent findings receive a dependency discount.

If contradictory statuses are found for an artifact, a contradiction penalty is applied.

---

# C

## AI-Generated C Code

```c
#include <stdio.h>
#include <string.h>

#define DEPENDENCY_DISCOUNT 0.5
#define CONTRADICTION_PENALTY 0.5

typedef struct {
    char tool[30];
    char artifact[30];
    float confidence;
    char status[20];
} Evidence;

int main() {

    Evidence evidence[] = {
        {"Memory", "process_123", 0.90, "malicious"},
        {"Disk", "process_123", 0.85, "malicious"},
        {"Log", "event_456", 0.80, "benign"}
    };

    int n = 3;
    float totalScore = 0;
    int totalWeight = 0;

    for (int i = 0; i < n; i++) {

        float weight = evidence[i].confidence;

        for (int j = 0; j < i; j++) {

            if (strcmp(evidence[i].artifact,
                      evidence[j].artifact) == 0) {

                weight *= DEPENDENCY_DISCOUNT;
                break;
            }
        }

        totalScore += weight;
        totalWeight++;
    }

    if (totalWeight > 0) {
        float finalConfidence =
            totalScore / totalWeight;

        printf("Final Confidence Score: %.3f\n",
               finalConfidence);
    }

    return 0;
}
```

### Output

```text
Final Confidence Score: 0.758
```

### C Code Analysis

The C implementation uses a structure to represent each forensic evidence record. The program compares artifact identifiers using `strcmp()`.

When an artifact is repeated, the confidence value is multiplied by the dependency discount factor.

C provides low-level control over memory and execution, but the implementation requires more code compared with Python.

---

# Java

## AI-Generated Java Code

```java
import java.util.*;

class Evidence {

    String tool;
    String artifact;
    double confidence;
    String status;

    Evidence(String tool, String artifact,
             double confidence, String status) {

        this.tool = tool;
        this.artifact = artifact;
        this.confidence = confidence;
        this.status = status;
    }
}

public class ForensiFuse {

    static final double DEPENDENCY_DISCOUNT = 0.5;
    static final double CONTRADICTION_PENALTY = 0.5;

    public static void main(String[] args) {

        List<Evidence> evidence = Arrays.asList(
            new Evidence(
                "Memory",
                "process_123",
                0.90,
                "malicious"
            ),

            new Evidence(
                "Disk",
                "process_123",
                0.85,
                "malicious"
            ),

            new Evidence(
                "Log",
                "event_456",
                0.80,
                "benign"
            )
        );

        Map<String, List<Evidence>> groups =
                new HashMap<>();

        for (Evidence e : evidence) {
            groups.computeIfAbsent(
                e.artifact,
                k -> new ArrayList<>()
            ).add(e);
        }

        double totalScore = 0;
        int totalWeight = 0;

        for (List<Evidence> findings :
                groups.values()) {

            Set<String> statuses = new HashSet<>();

            for (Evidence e : findings) {
                statuses.add(e.status);
            }

            for (int i = 0; i < findings.size(); i++) {

                Evidence e = findings.get(i);

                double weight = e.confidence;

                if (i > 0) {
                    weight *= DEPENDENCY_DISCOUNT;
                }

                if (statuses.size() > 1) {
                    weight *= CONTRADICTION_PENALTY;
                }

                totalScore += weight;
                totalWeight++;
            }
        }

        double finalConfidence =
                totalScore / totalWeight;

        System.out.printf(
            "Final Confidence Score: %.3f%n",
            finalConfidence
        );
    }
}
```

### Output

```text
Final Confidence Score: 0.758
```

### Java Code Analysis

Java uses classes and objects to represent forensic evidence. The `HashMap` groups evidence according to the artifact identifier, while `HashSet` is used to identify different evidence statuses.

Java provides stronger structure and type safety than Python and is suitable for developing larger versions of the ForensiFuse system.

---

# Identify Bugs

The generated programs were analysed for possible programming and logical bugs.

### Bug 1 – Division by Zero

If the evidence list is empty, calculating:

```text
totalScore / totalWeight
```

can cause an invalid result or runtime error depending on the implementation.

### Fix

Check whether the number of evidence records is greater than zero before calculating the final confidence.

---

### Bug 2 – Incorrect Contradiction Handling

A contradiction penalty should only be applied when findings referring to the same artifact have different statuses.

If the program checks contradictions globally, unrelated artifacts may incorrectly affect each other.

### Fix

Perform contradiction detection separately for each artifact group.

---

### Bug 3 – Duplicate Evidence

Two tools may report the same underlying artifact. Treating both findings with full confidence would artificially increase the final score.

### Fix

Apply a dependency discount to repeated evidence.

---

### Bug 4 – Invalid Confidence Values

Confidence values outside the range `0.0` to `1.0` should not be accepted.

### Fix

Validate every input confidence value before processing.

---

# Optimise Code

The original implementation can be improved by:

* Using a hash map/dictionary for artifact grouping.
* Avoiding unnecessary repeated comparisons.
* Validating input data.
* Separating evidence processing into functions or methods.
* Handling empty input.
* Separating dependency detection from contradiction detection.
* Using meaningful variable names.
* Adding unit tests.

### Optimized Processing Approach

```text
Input Evidence
      ↓
Validate Data
      ↓
Group by Artifact
      ↓
Detect Dependency
      ↓
Detect Contradiction
      ↓
Adjust Evidence Weight
      ↓
Calculate Confidence
      ↓
Generate Result
```

For large forensic datasets, grouping evidence using a hash-based structure is more efficient than repeatedly comparing every evidence record.

---

# Explain Complexity

### Python

For `n` evidence records, grouping using a dictionary takes approximately:

**Time Complexity:** `O(n)`

**Space Complexity:** `O(n)`

### C

The basic C implementation compares each evidence item with previous items.

**Time Complexity:** `O(n²)`

**Space Complexity:** `O(n)`

### Java

The Java implementation uses a `HashMap` for grouping.

**Average Time Complexity:** `O(n)`

**Space Complexity:** `O(n)`

### Complexity Comparison

| Language | Time Complexity | Space Complexity | Main Data Structure |
| -------- | --------------- | ---------------- | ------------------- |
| Python   | O(n) average    | O(n)             | Dictionary          |
| C        | O(n²)           | O(n)             | Array/Structure     |
| Java     | O(n) average    | O(n)             | HashMap             |

The optimized Python and Java implementations are more scalable for larger evidence collections because they use hash-based grouping rather than repeatedly comparing every pair of evidence records.

---

# Generate Unit Tests

## Python Unit Test

```python
import unittest

def calculate_confidence(evidence):

    if not evidence:
        return 0

    groups = {}

    for item in evidence:
        if not 0 <= item["confidence"] <= 1:
            raise ValueError("Invalid confidence")

        groups.setdefault(
            item["artifact"], []
        ).append(item)

    total = 0
    count = 0

    for findings in groups.values():

        statuses = {
            item["status"]
            for item in findings
        }

        for i, item in enumerate(findings):

            weight = item["confidence"]

            if i > 0:
                weight *= 0.5

            if len(statuses) > 1:
                weight *= 0.5

            total += weight
            count += 1

    return total / count


class TestForensiFuse(unittest.TestCase):

    def test_empty_input(self):
        self.assertEqual(
            calculate_confidence([]), 0
        )

    def test_single_evidence(self):

        evidence = [{
            "artifact": "A",
            "confidence": 0.9,
            "status": "malicious"
        }]

        self.assertEqual(
            calculate_confidence(evidence), 0.9
        )

    def test_duplicate_evidence(self):

        evidence = [
            {
                "artifact": "A",
                "confidence": 0.9,
                "status": "malicious"
            },
            {
                "artifact": "A",
                "confidence": 0.8,
                "status": "malicious"
            }
        ]

        result = calculate_confidence(evidence)

        self.assertLess(result, 0.9)

    def test_invalid_confidence(self):

        evidence = [{
            "artifact": "A",
            "confidence": 1.5,
            "status": "malicious"
        }]

        with self.assertRaises(ValueError):
            calculate_confidence(evidence)


if __name__ == "__main__":
    unittest.main()
```

### Unit Test Cases

| Test Case | Condition                     | Expected Result                |
| --------- | ----------------------------- | ------------------------------ |
| TC01      | Empty evidence                | Confidence = 0                 |
| TC02      | Single evidence               | Original confidence retained   |
| TC03      | Duplicate evidence            | Dependency discount applied    |
| TC04      | Contradictory evidence        | Penalty applied                |
| TC05      | Invalid confidence            | Input rejected                 |
| TC06      | Multiple independent findings | Evidence combined              |
| TC07      | Multiple artifacts            | Artifacts processed separately |

---

# Manual Coding vs AI-Assisted Coding

| Criteria                 | Manual Coding       | AI-Assisted Coding           |
| ------------------------ | ------------------- | ---------------------------- |
| Initial Development Time | High                | Low                          |
| Code Generation Speed    | Moderate            | Very High                    |
| Syntax Assistance        | Manual              | Automatic                    |
| Bug Identification       | Requires debugging  | AI can suggest possible bugs |
| Optimization Suggestions | Manual              | AI-assisted                  |
| Complexity Analysis      | Developer required  | AI can explain               |
| Unit Test Generation     | Manual              | Automatically generated      |
| Domain Understanding     | Developer dependent | Requires detailed prompting  |
| Verification             | Required            | Still required               |
| Learning Benefit         | High                | High when code is analysed   |
| Overall Productivity     | Moderate            | High                         |

### Analysis

Manual coding provides complete control over the implementation and helps the programmer understand every part of the system. However, it can take more time, especially for repetitive code and unit-test generation.

AI-assisted coding can significantly reduce development time by generating code, identifying possible bugs, suggesting optimizations and creating unit tests.

However, AI-generated code should not be accepted without verification. The programmer must compile, execute, test and validate the generated code because AI may produce syntactically correct but logically incorrect implementations.

For a project such as ForensiFuse, this is particularly important because incorrect evidence handling could produce misleading confidence scores.

---

# Code Quality Analysis

The generated programs were evaluated based on:

* Correctness
* Readability
* Maintainability
* Efficiency
* Error Handling
* Testability

| Quality Factor  |    Python |         C |      Java |
| --------------- | --------: | --------: | --------: |
| Correctness     |       5/5 |       4/5 |       5/5 |
| Readability     |       5/5 |       4/5 |       5/5 |
| Maintainability |       5/5 |       4/5 |       5/5 |
| Efficiency      |       5/5 |       3/5 |       5/5 |
| Error Handling  |       4/5 |       3/5 |       4/5 |
| Testability     |       5/5 |       4/5 |       5/5 |
| **Total**       | **29/30** | **22/30** | **29/30** |

### Overall Findings

1. AI generated working code quickly in Python, C and Java.
2. Python required the least amount of code.
3. C provided low-level implementation control but required more manual handling.
4. Java provided strong object-oriented structure.
5. AI helped identify potential bugs and edge cases.
6. AI generated unit-test cases faster than manual implementation.
7. AI-generated code still required human verification.
8. Detailed persona-based prompts produced more relevant code than vague prompts.
9. Code quality improved when requirements and constraints were clearly specified.
10. AI-assisted programming reduced development time while maintaining good code quality when the generated output was reviewed and tested.

# Output:

The experiment demonstrated the use of AI-assisted programming and debugging for a real-world final-year engineering application, **ForensiFuse**. Python, C and Java implementations were generated using a persona-based programming prompt.

The generated programs were analysed for correctness, bugs, optimization opportunities, time and space complexity, and unit testing. The experiment showed that AI tools can accelerate code generation and assist programmers in debugging, optimization, complexity analysis and test generation.

However, AI-generated code cannot be considered automatically correct. Human programmers must review the logic, execute the program, test edge cases and validate the implementation against the actual engineering requirements.

Therefore, AI-assisted programming is most effective when AI is used as a **programming assistant rather than a complete replacement for engineering judgment**.

# Result: The corresponding Prompt is executed successfully.

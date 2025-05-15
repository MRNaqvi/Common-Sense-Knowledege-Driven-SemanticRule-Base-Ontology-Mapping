# Common Sense Knowledge-Driven Semantic Rule-Based Ontology Mapping

This project leverages the Owlready2 library and OpenAI's language models to support the generation and integration of semantic rules into OWL/RDF ontologies. It is designed for researchers in knowledge engineering and semantic web technologies aiming to automatically convert commonsense knowledge (CSK) into logical rules for ontology enrichment.

---

## Overview

The system supports:
- **Ontology Loading and Manipulation** using Owlready2
- **Commonsense Knowledge Generation** using LLMs (via OpenAI API)
- **Rule Template Specialization**: Mapping natural language CSK to formal rules (FOL/SPARQL)
- **Ontology Exporting**: Save updated ontologies in RDF/XML format

A **chain-of-thought prompt engineering** strategy is used to generate high-quality natural language CSK, which is then mapped to logical rule templates (e.g., SWRL).

---

## Key Features

- **Commonsense Knowledge Generation** (via OpenAI LLMs)
- **Ontology Import and Manipulation** (Owlready2)
- **Dynamic Class and Instance Creation**
- **Rule Template Definition and Specialization**
- **Export of Enriched Ontologies**
  
---

## Prerequisites

- Python 3.7+
- [OpenAI API Key](https://platform.openai.com/)
- Libraries:
  - `owlready2`
  - `pandas`
  - `openai`

Install required packages:
```bash
pip install owlready2 pandas openai


Installation
bash
Copy
Edit
git clone https://github.com/MRNaqvi/Common-Sense-Knowledege-Driven-SemanticRule-Base-Ontology-Mapping.git
cd Common-Sense-Knowledege-Driven-SemanticRule-Base-Ontology-Mapping
📦 Usage
1. Load Ontologies
python
Copy
Edit
from owlready2 import get_ontology

ontology = get_ontology("path/to/core.rdf").load()
ontology = get_ontology("path/to/bfo.owl").load()



### 2. Dynamically Add Classes/Instances
python
Copy
Edit
from owlready2 import types

NewClass = types.new_class("PaintedObject", (ontology.ExistingParentClass,))
new_instance = NewClass("Object_123")



### 3. Generate Commonsense Knowledge using OpenAI

import openai
import os

openai.api_key = os.getenv("OPENAI_API_KEY")

response = openai.ChatCompletion.create(
  model="gpt-4",
  messages=[{"role": "user", "content": "Painting results in a painted object"}]
)

print(response.choices[0].message['content'])


###4. Apply Rule Template
python
Copy
Edit
from your_module import RuleTemplate, CSK, SpecializeRule

# Define a template rule in FOL
template = RuleTemplate("∀x (process(x) → ∃y (product(y) ∧ isOutputOf(x, y)))")

# Define a CSK statement
csk = CSK("Painting results in a painted object.")

# Specialize the rule
concrete_rule = SpecializeRule(template, csk)

print(concrete_rule)


###5. Save the Ontology

ontology.save(file="output/enriched_ontology.rdf", format="rdfxml")


@@@@Notes
We use prompt chaining to improve the reliability of CSK statements from LLMs.

Rule templates are designed manually and then specialized using extracted class/instance information from CSK.

## Overview

Thissystem leverages the Owlready2 library to manage and manipulate ontologies for semantic rule application. It's designed to support researchers and developers in fields like knowledge engineering, providing tools for ontology loading, updating, rule application, and exporting.

## Key Features
- **OPENAIAPi**: For Generating Commonsense Knwoledge Statements*
- **Load Ontologies**: Load RDF/OWL ontologies for manipulation.
- **Dynamic Updates**: Add new classes and instances to existing ontologies.
- **Semantic Rule Application**: Apply common sense knowledge rules to enhance ontology.
- **Export Ontologies**: Save updated ontologies back to RDF/XML format.
        
Note : Chain of tought Prompt Engineering Method has been used to get exact NL CSK statement that process late to create FOL and SPARQL.                      
## Prerequisites
-OPENAI API
- Python 3.x
- Owlready2
- Pandas

Install the required Python packages using pip:

```bash
pip install owlready2 pandas

##Installation
-To set up the project, clone this repository and navigate into the project directory:

git clone https://github.com/MRNaqvi/Common-Sense-Knowledege-Driven-SemanticRule-Base-Ontology-Mapping.git
cd Common-Sense-Knowledege-Driven-SemanticRule-Base-Ontology-Mapping

##Usage
-Loading the Ontology
Import the ontology from an file:

from owlready2 import get_ontology

ontology = get_ontology("path/to/your/core.rdf").load()
ontology = get_ontology("path/to/your/bfo.owl").load()


##Manipulating the Ontology
Add new classes and instances dynamically:

from owlready2 import types

# Assuming 'ExistingParentClass' is a valid class in your ontology
new_class = types.new_class("NewClassName", (ontology.ExistingParentClass,))
new_instance = new_class("NewInstanceName")



import openai

openai.api_key = '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'

response = openai.ChatCompletion.create(
  model="gpt-4",
  messages=[
        {"role": "user", "content": "What is Common Sense Knowledge?"}
    ]
)

print(response.choices[0].message['content'])

Note : Chain of tought Prompt Engineering Method has been used to get exact NL CSK statement that process late to create FOL and SPARQL. 

#Defining and Applying Rule Templates
#Create rule templates and apply them based on specific domain knowledge:

from your_module import RuleTemplate, CSK, SpecializeRule

#Define a rule template
rt = RuleTemplate("∀x (process(x) → ∃y (product(y) ∧ isOutputOf(x, y)))")

# Define common sense knowledge Statement

csk = CSK("Painting results in a Painted Object")

#Apply the rule to generate a concrete rule

concrete_rule = SpecializeRule(rt, csk)

print(concrete_rule)

#Saving the Ontology



-Save the updated ontology back to an RDF/XML format:
ontology.save(file="path/to/saved_ontology.rdf", format="rdfxml")




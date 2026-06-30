# AI Evaluation Prompts

## Primary Evaluation Prompt

This is the prompt used to evaluate Copilot responses for quality and compliance.22

You will evaluate the following Copilot response against three criteria:

Grounding: Is the response based only on information in our knowledge base?
Scope: Does it answer the user's actual question?
Confidence: Is the stated confidence level appropriate?

Respond ONLY with this JSON format:
{
"score": [1-10],
"grounded": true or false,
"in_scope": true or false,
"confidence_appropriate": true or false,
"reasoning": "[brief explanation of score]"
}
Rules:

If ANY criteria fail, score must be below 8
If grounded = false, maximum score is 4
If in_scope = false, maximum score is 5
Never make assumptions about information not in the knowledge base
## Sample Responses

### Example 1: Good Response (Score: 9)
{
"score": 9,
"grounded": true,
"in_scope": true,
"confidence_appropriate": true,
"reasoning": "Response directly answers question using only approved knowledge base. Confidence level matches quality."
}
### Example 2: Hallucination (Score: 3)
{
"score": 3,
"grounded": false,
"in_scope": true,
"confidence_appropriate": false,
"reasoning": "Response contains information not in knowledge base (hallucination). Stated with high confidence despite uncertainty."
}
### Example 3: Out of Scope (Score: 6)
{
"score": 6,
"grounded": true,
"in_scope": false,
"confidence_appropriate": true,
"reasoning": "Response is accurate but addresses tangential topic, not the user's actual question. Needs human review."
}
## Guardrails Applied

✓ **Specificity:** Prompt only evaluates against defined criteria  
✓ **Structure:** Forces JSON response (not free-form)  
✓ **Boundaries:** Clear rules about what disqualifies a response  
✓ **Transparency:** Reasoning required for every score
## Guardrails Applied

✓ **Specificity:** Prompt only evaluates against defined criteria  
✓ **Structure:** Forces JSON response (not free-form)  
✓ **Boundaries:** Clear rules about what disqualifies a response  
✓ **Transparency:** Reasoning required for every score
## Guardrails Applied

✓ **Specificity:** Prompt only evaluates against defined criteria  
✓ **Structure:** Forces JSON response (not free-form)  
✓ **Boundaries:** Clear rules about what disqualifies a response  
✓ **Transparency:** Reasoning required for every score

## Part 2: Prompt Log Continued (Week 10)

### Entry 6: Building an Error Catch Workflow in n8n
**Context:** During Checkpoint 2 bulk testing, our Groq API calls occasionally timed out, causing the entire n8n execution to fail silently. I needed Copilot to help build a graceful failure path.
**Prompt:** > I have an n8n workflow making an HTTP request to Flowise. Sometimes it fails due to rate limits. How do I capture the exact error message and route the failed execution data to an Airtable update node instead of just stopping the workflow?
**Result:** Copilot explained how to use the "Error Trigger" node or toggle "Continue On Fail" in the HTTP node settings, then use an IF node to check `{{$json.error}}`.
**Evaluation:** The "Continue On Fail" toggle paired with an IF node was the cleanest solution for our specific component architecture.
**What I changed:** I routed the false branch of the IF node directly to Airtable, passing the specific API error message into our new `error_reason` text field.
**What I learned:** Error handling in n8n is much easier when managed at the node level rather than trying to build entirely separate catch workflows.

### Entry 7: Designing Airtable Dashboard Filters
**Context:** I needed to create the two required dashboard views for Week 10. The manual triage view needed a complex filter to catch both API errors and low confidence AI scores.
**Prompt:**
> I am building an Airtable view for Error Monitoring and Manual Triage. I need a filter formula that captures records where the status field exactly equals "error", OR where the relevance_score is less than 65, OR where the indicators field contains the string "None".
**Result:** Copilot provided the exact Airtable filter formula: `OR({status} = "error", {relevance_score} < 65, FIND("None", {indicators}))`.
**Evaluation:** The formula worked perfectly on the first try and properly grouped all our edge cases into one view.
**What I changed:** I added an additional parameter to also flag records where the severity was blank, just in case the Flowise JSON output was malformed.
**What I learned:** Writing nested logical formulas in Airtable can be tedious, and Copilot generates the correct syntax instantly as long as you provide the exact field names.

### Entry 8: Structuring Confidence Routing Logic
**Context:** We needed to build the logic for the IF node to route high priority threats to the main dashboard and everything else to a review queue.
**Prompt:**
> Write an n8n expression for an IF node. It should output true if the incoming JSON data has a severity of 'critical' or 'high', AND a relevance_score of 65 or greater. It should output false for anything else.
**Result:** Copilot generated a clean JavaScript expression evaluating the incoming `$json` parameters against the thresholds.
**Evaluation:** The generated expression was accurate and accounted for potential casing issues by converting the severity string to lowercase before comparing.
**What I changed:** I removed the explicit strict equality check and used `includes()` for the severity string to account for potential whitespace issues from the AI output.
**What I learned:** Having Copilot draft the n8n expressions directly prevents simple syntax errors from breaking the routing logic during active testing.
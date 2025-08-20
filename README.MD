# n8n-sales-brief

> A demonstration of generating a sales prep brief in n8n, combining data from Apollo.io and Gemini, then saving to a Google Doc.

## Setup instructions

* Add your Gemini API key.
* Add your Google Drive credentials.
* Add your Apollo.io API key (available on the free tier).
* Review and adjust the prompt in "Company Research Prompt" as needed.
* Add the Drive folder ID into "Destination preferences".

## The approach

* I have chosen a form input as an easy way to get variables into the flow (but assume this would be replaced with a sales tool trigger in production).
* The flow combines structured data from Apollo.io with Gemini's knowledge to create the brief. The Apollo API requires a domain name to do this search, so a quick lookup is needed before we can do the main enrichment search. In production we would probably alredy have the domain name from the email in the contact record.
* Though I believe the best output location would be inside the company's sales tool, I've saved the output to a Google Doc as it's a widely used tool that also provides useful functions like converting HTML to Docs and Docs to PDF, which this workflow uses. _Google Docs formatting is not straightforward in n8n_, so I've used an HTTP node to upload HTML to Drive and convert it to a Google Doc on the fly.
* You can see a sample PDF inside `sample_reports` in this repo or find a [sample Google Drive file here](https://docs.google.com/document/d/1QxB7Ap57O-SP1ZBcqZf7glmBJU_pXtOh7TLHr7HAusw/edit?tab=t.0).

## Assumptions made

* I assume the sales team would be able to provide guidance on the content of the sales prep brief. In the meantime, I have made some basic guesses. Much more data is available in Apollo than the flow currently uses, so that would be an easy enhancement.
* I assume HubSpot or a similar sales tool is used to manage the sales pipeline, which would provide triggers and initial data for the workflow in production.

## Limitations of this solution

* If the workflow is run multiple times with the same company input, duplicate files would be created in Google Drive.
* There is no disambiguation for domain names, so better handling would be needed (or, ideally, just use the domain name from the contact email in the sales record).

## How I would improve it if I had more time

* Consider integrating more research inputs (for example, Clearbit and BuiltWith) and incorporating them into the report, depending on the needs of the sales team.
* Consider the ideal workflow trigger and where the data should ultimately appear. As above, I think this would most likely be triggered by a sales pipeline stage changing, and the data would be added directly to the deal record inside the sales tool (e.g., HubSpot) to ensure the data is where the sales agents need it.
* Consider the pros and cons of using tool calls vs. a standalone node to generate the sales prep brief.
* Improve the appearance of the report and include links to additional references.
* Fix the limitations listed above.

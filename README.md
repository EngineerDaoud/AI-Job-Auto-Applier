# ApplyPilot AI

**Project:** AI Job Auto Applier (n8n workflow)

Give it a company website, and an AI agent writes a personalized job application email based on your skills and sends it for you.

## What it does

ApplyPilot AI automates job applications. You submit a target company website and the role you are applying for. The workflow scrapes the site, extracts the company's contact email and a short business summary, then an AI agent reads your experience from a Google Sheet, writes a tailored email and sends it through Gmail.

## Workflow

```
Form -> Get Website -> HTML to Markdown -> Information Extractor (Gemini)
     -> If (email found?)
          Yes -> AI Agent (tools: Google Sheet experience, Gmail send) -> Completion message
          No  -> Stop
```

| Step | Node | Description |
|------|------|-------------|
| 1 | Submit Data (Form) | Fields: `Target Business Websites` and an `Apply As` dropdown (AI Automation Engineer, MERN Stack Web Developer, Graphic Designer Expert) |
| 2 | Get Website | Fetches the website HTML |
| 3 | Markdown | Converts the HTML to clean markdown |
| 4 | Information Extractor | Gemini extracts the company **email** and a 1-2 sentence **summary** |
| 5 | If | Stops the run if no valid email (`@`) was found |
| 6 | AI Agent | Writes the subject and body using the company info and the selected role |
| 7 | GET Experience and Skill | Agent tool that reads your experience and skills from a Google Sheet |
| 8 | Send a message in Gmail | Agent tool that sends the email |
| 9 | Feedback | Shows the result on the form completion page |

## Setup

### Requirements
- n8n (cloud or self-hosted)
- Google Gemini API key
- Gmail account (OAuth2)
- A Google Sheet containing your experience and skills

### Steps
1. In n8n go to **Workflows -> Import from File** and select `workflow.json`.
2. Connect credentials: Google Gemini (PaLM), Google Sheets and Gmail.
3. In the **GET Experience and Skill** node, select your own experience sheet.
4. In the **AI Agent** system prompt, update the name, email and phone number.
5. Activate the workflow, open the form URL and submit a website and a role.

## Customization

- Add new roles by editing the dropdown options in the **Submit Data** form.
- Change the email tone or length in the **AI Agent** system message.
- Swap Gemini for another model by replacing the chat model nodes.

## Tips

- The agent sends the email directly, so test with your own address first.
- The more detailed your experience sheet is, the more personalized the emails will be.

## Author

Muhammad Daoud, AI Automation Engineer

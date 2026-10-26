# Lab prompts

Copy each prompt with the copy button on the right of the box. Paste it into **claude.ai/code** (not the normal Claude chat).

## Setup check
```
List the files in data/raw.
```
Expected: `telco_v2.csv`.

## Step 0. Know the data
```
Profile data/raw/telco_v2.csv. Show me: row count, unique customer IDs, each column's type, min and max of every number column, blanks per column, and churn rate by every column. Do not clean or change anything.
```
Then write down 3 things that look wrong. Keep them for Step 4.

## Step 1. Brief by interview
```
Interview me one question at a time to write briefs/2m-campaign.md for this decision: should we fund a $2M campaign to move month-to-month customers to 1-year contracts? Cover: the decision, the questions to answer, data checks, analysis, when to stop and ask me, and what to deliver. Push back if my answer is vague. Then write the file.
```
Give specific answers. The gray text in the prompt box is only a suggestion.

## Step 2. Reviewer agent
```
Create a subagent called reviewer. It acts like a senior analyst who did not do the work. It checks every number in recommendation.md against the raw data, flags any causal claim, flags any data problem the analysis missed, and writes its review to runs/telco/review.md. It can read files and run code, but it cannot edit the analysis. Create only the agent file. No hooks or other files.
```

## Step 3. Run in Plan mode
First click **Auto** under the prompt box and choose **Plan** (or press `3`). Check that it says **Plan**.
```
Follow CLAUDE.md and briefs/2m-campaign.md. Do the analysis and write all deliverables. When done, ask the reviewer agent to review it. Report its verdict. Do not fix anything yet.
```
To change a step in the plan, type the change as a normal message. Example:
```
In the sizing step, show how many customers must stay to pay back $2M.
```

## Step 4. Verify with evidence
The prompt for this step is on the slide.

## Step 5. Deliver
```
Fix only the must-fix items the review flagged. Then commit everything with the message "Session 1 run" and push to GitHub.
```
Push failed with a 403 error? The Claude GitHub app has no access to your repo. Ask for help.

Then submit your name and repo link: https://forms.gle/CzgbPNLwc2AJMQLXA

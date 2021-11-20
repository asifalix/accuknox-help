## Slack Integration
Channel Integrations is the fourth sub-section of Workspace Manager.

This section is used to integrate external services with AccuKnox and export logs based on triggers.

 1. Slack

Choose "Slack" services and click the <b>Integrate Now</b> button.

### 1. Integration of Slack:
#### a. Prerequisites:
- You need a valid and active account in Slack.
- After logging into your Slack channel, you must generate a Hook URL.
- [Note]: If you don’t know how to get Hook URL then click this [link](https://slack.com/intl/en-in/help/articles/115005265063-Incoming-webhooks-for-Slack) and follow the steps.

#### b. Steps to Integrate:
- Goto Channel Integration [URL](https://app.dev.accuknox.com/channel-integrations)
- Click the Integrate Now button -> Slack
- Here you'll be able to see these entries:
  - <b>Integration Name:</b> Enter the name for the integration. You can set any name.
  - <b>Hook URL:</b> Enter your slack hook URL here.
  - <b>Sender Name:</b> Enter the sender name here.
  - <b>Channel Name:</b> Enter your slack channel name here.
  - <b><i>Message Title:</i></b> You can set a message title using this input field. <i>This is optional.</i>
  - <b><i>Tags to be sent with alerts:</i></b> You can set tags using this input field. <i>This is optional.</i>
- Once you fill every field then click the button this will test whether your integration is working or not.
- Click the Save button.

### 2. Configuration of Alert Triggers:
- On the Logs page, after choosing specific log filter click on 'Create Trigger' button.
- The below fields needs to be entered with appropriate data:
  - <b>Name:</b> Enter the name for the trigger. You can set any name without special characters.
  - <b>When to Initiate:</b> The frequency of the trigger as Real Time / .
  - <b>Status:</b> Enter the severity for the trigger.
  - <b>Search Filter Data :</b> The filter log chosen in automatically populated here.<i>This is optional.</i>
  - <b>Predefined queries:</b> The list of predefined queries for this workspace is shown as default.
  - <b>Notification Channel:</b> Select the integration channel that needs to receive logs. This should be Slack. (Note: Channel Integration is done on the previous step)
  - <b>Save:</b> Click on Save for the trigger to get stored in database.

### 3. Logs Forwarding:
- For each Enabled Trigger, please check the Slack channel to view the logs.
  - Based on Frequency (Real Time / Once in a Day / Week)
- The Rule Engine matches the real time logs against the triggers created.

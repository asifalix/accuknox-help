## AWS CloudWatch Integration
Channel Integrations is the fourth sub-section of Workspace Manager.

This section is used to integrate external services with AccuKnox and export logs based on triggers.

 1. AWS CloudWatch

Choose "AWS CloudWatch" services and click the <b>Integrate Now</b> button.


### 1. Integration of Amazon CloudWatch:
#### a. Prerequisites
 - AWS Access Key / AWS Secret Key is required for this Integration.
 - <b>[Note]:</b> Please refer this link to create access keys [link](https://signin.aws.amazon.com/)

#### b. Steps to Integrate:
 - Goto Channel Integration [URL](https://app.dev.accuknox.com/channel-integrations)
 - Click the Integrate Now button -> AWS CloudWatch
 - Here you'll be able to see these entries:
    - <b>Integration Name:</b> Enter the name for the integration. You can set any name.
    - <b>AWS Access Key:</b> Enter your AWS Access Key here.
    - <b>AWS Secret Key:</b> Enter your AWS Secret Key here.
    - <b>Region Name:</b> Enter your AWS Region Name here.
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
  - <b>Notification Channel:</b> Select the integration channel that needs to receive logs. This should be AWS CloudWatch. (Note: Channel Integration is done on the previous step)
  - <b>Save:</b> Click on Save for the trigger to get stored in database.

### 3. Logs Forwarding:
- For each Enabled Trigger, please check the AWS platform to view the logs.
  - Based on Frequency (Real Time / Once in a Day / Week)
- The Rule Engine matches the real time logs against the triggers created.

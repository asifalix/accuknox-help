## Splunk Integration
Channel Integrations is the fourth sub-section of Workspace Manager.

This section is used to integrate external services with AccuKnox and export logs based on triggers.

 1. Splunk

Choose "Splunk" services and click the <b>Integrate Now</b> button.


### 1. Integration of Splunk:
#### a. Prerequisites
 - You need a Splunk HTTP event collector URL for this Integration.
 - <b>[Note]:</b> If you don’t know how to get Splunk HTTP event collector URL then click this [link](https://docs.splunk.com/Documentation/SplunkCloud/8.2.2106/Data/UsetheHTTPEventCollector)

#### b. Steps to Integrate:
 - Goto Channel Integration [URL](https://app.dev.accuknox.com/channel-integrations)
 - Click the Integrate Now button -> Splunk
 - Here you'll be able to see these entries:
    - <b>Integration Name:</b> Enter the name for the integration. You can set any name.
    - <b>Splunk HTTP event collector URL:</b> Enter your Splunk HTTP event collector URL here.
    - <b>Token:</b> Enter your Splunk Token here.
    - <b>Source:</b> Enter your Splunk Source here.
    - <b>Index:</b> Enter your Splunk Index here.
    - <b>Source Type:</b> Enter your Source Type here.
    - <b>Enable HTTPS:</b> If you want HTTPS service then enable this button.
    - <b>Enable TLS Verify:</b> If you want TLS service then enable this button.
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
  - <b>Notification Channel:</b> Select the integration channel that needs to receive logs. This should be Splunk. (Note: Channel Integration is done on the previous step)
  - <b>Save:</b> Click on Save for the trigger to get stored in database.

### 3. Logs Forwarding:
- For each Enabled Trigger, please check the Splunk channel to view the logs.
  - Based on Frequency (Real Time / Once in a Day / Week)
- The Rule Engine matches the real time logs against the triggers created.

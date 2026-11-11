Experiment 5 – Slack Integration with Jenkins, following your handwritten lab procedure in the same order.

We'll use:

* Jenkins on Windows

* Slack workspace

* Public Slack channel: `demo-1`

* Jenkins Freestyle Project: `demo123`

* Slack Notification plugin

### Experiment 5 – Integration of Jenkins with Slack

Aim: To integrate Jenkins with Slack to send automated notifications about successful and failed builds.

### Part 1 – Configure Slack

### Step 1: Login to Slack

* Open [Slack](https://slack.com/?utm_source=chatgpt.com).

* Login to your account.

* Open your workspace.

### Step 2: Create a channel

![Slack Live Chat Integration - Social Intents Knowledge Base](https://images.openai.com/static-rsc-4/9OIEFsuD28JHYmxDcPNQ6y6K5iS06rAW6IygvGQV_3daQBNKp-4mdnP7FLMrdItDs5PN7S0DwGAoQxaTx_j64TS6iuxTg6L5OdpAVYl2LfPruJQGthKCIaYOZF_uyRMNETcp_KHWMO2UDk-jh879Oajxodw6ICn6W8Ma-1-cpYfOOhDFlC3xo5Hn3uK9LSFE?purpose=fullsize)

* Click the `+` beside Channels.

* Select Create a channel.

* Enter channel name:

```text
demo-1
```

* Select Public.

* Click Create.

### Step 3: Add Jenkins CI app to Slack

![如何為 Slack 設定 Jenkins 通知 ? | 點燈坊](https://images.openai.com/static-rsc-4/tSe0sEXfxY23BwaYzP1iNO6tERa3qyBwDMQpypcg5NE8Iyapju3225GAgS294ToM0DhyaLm7boPzNHFJYuUedCLC8RtqNbxgptW7t3hrgfDBBsjCM4oJc2MQERsPMCDkuXScxlMxz443Y4hGR46YokcuO8wdffx9Apn33vCzE0kuz1d_B-Re6GsL5RoKmQMk?purpose=fullsize)

* In Slack, open Apps.

* Search for `Jenkins CI`.

* Open Jenkins CI.

* Click Add to Slack.

* Review permissions and approve.

* Select your created channel `demo-1`.

* Click Add Jenkins CI Integration.

This is the Jenkins CI integration mentioned in your notebook. Slack Marketplace +1

Important: The older Jenkins CI integration uses an integration token. The current Jenkins plugin also supports a newer custom Slack app with a bot token. Don't mix the two configurations. I'll explain the correct choice below.

### Step 4: Copy the Slack integration token

After adding the integration:

* Slack should show the Jenkins CI integration configuration.

* Find the integration token.

* Copy the token and keep it private.

Never share your token in screenshots.

If Slack doesn't show an integration token and instead provides a Bot User OAuth Token starting with `xoxb-`, use the modern custom-app method described in the note below.

### Part 2 – Configure Jenkins

### Step 5: Install Slack Notification plugin

![See Build Status in Slack With Jenkins-Slack Integration](https://images.openai.com/static-rsc-4/DwjrRtnVyOP9Rutavz-45BJ0ibbqFlE9JnK38HVkcmFLwWOLEFWycqK5ACOxlAYvWN17_G5aCRXD5APBphZVurPt0_9YgM1lZmTnwXZQWRg-hPuUtGkfUb4OqS-5Kk28vqVqO8fu_lkk9EKtsP6W1n4N-U5O_wz2rIidbXHoBSwWvbHpO2zkvp4bCXoZ0LJT?purpose=fullsize)

1\. Open Jenkins:

```text
http://localhost:8080
```

* Click Manage Jenkins.

* Click Plugins.

* Select Available plugins.

* Search for:

```text
Slack Notification
```

* Select the plugin.

* Click Install.

* Wait until installation completes.

The plugin enables Jenkins to send build notifications to Slack. Jenkins plugin

### Step 6: Configure Jenkins system settings

* Go to Manage Jenkins.

* Click System.

* Scroll down to the Slack section.

Fill in:

| Field                      | Value                     |
| -------------------------- | ------------------------- |
| Workspace / Team Subdomain | Your Slack workspace name |
| Default channel            | #demo-1                   |
| Credentials                | Your saved Slack token    |

How to find your workspace name?

Open Slack in your browser and check the workspace URL. Use only the workspace subdomain/name, not the complete URL.

### Step 7: Add Slack credentials

![Send notifications to Slack using Jenkins - DEV Community](https://images.openai.com/static-rsc-4/-uS9hv7byNUmh-1037HpnT7vMzqozzrUTxJKh-ncxsbz-JRNeBlen2a1ts_UdDoYgOl6a8CQTuCtcotXu2gt1iEoO_UYHsQuSFALswHiyoLaCtwaWIa5eYt9C2HoTyKXcMO8mdTsZWGRUqm76cHVfFcsSU80FNRSbIRAl7-KvZ-hJ5PrbOoJjYMKRDlDQ75s?purpose=fullsize)

Follow your notebook:

* Go to Manage Jenkins → Credentials.

* Open System.

* Click Global credentials.

* Click Add Credentials.

Enter:

| Field       | Value                         |
| ----------- | ----------------------------- |
| Kind        | Secret text                   |
| Scope       | Global                        |
| Secret      | Paste Slack integration token |
| ID          | slack-token                   |
| Description | Slack Integration             |

5\. Click Create.

Return to Manage Jenkins → System.

* Select `slack-token` in the Slack credentials dropdown.

* Click Test Connection.

Test connection successful.

8\. Click Save.

Token configuration note: If you're using a modern `xoxb-` bot token instead of the old Jenkins CI integration token, enable Custom Slack App Bot User in Jenkins and invite the bot into `demo-1`. The official plugin documentation describes this newer configuration. Jenkins plugin +1

### Part 3 – Create Jenkins project

### Step 8: Create a new item

![Integrating with Jenkins (freestyle) – TestRail Support Center](https://images.openai.com/static-rsc-4/qL9XxOksiROlr171eHEJiBAz4LClhJG4zNWhUP_zm7aUxKMOvSd4uqMP8pb7f3HLcQjl6aWCx9xc1J4B5jB-F8FoUPZhf1rXXESFZYFoKk5zZLtBeKEPOTyv8Yqvz4O9L_JBWokWmVNrocA6MBrU26AA7uZzES_CSYAuOabZR4qKcSZpbl1sKg7PAQcVfkZn?purpose=fullsize)

* Go to Jenkins Dashboard.

* Click New Item.

* Enter the project name:

```text
demo123
```

* Select Freestyle Project.

* Click OK.

### Step 9: Configure Build Steps

Scroll down to Build Steps.

* Click Add build step.

* Select Execute Windows batch command.

* Enter:

```bat
java -version
echo Jenkins build executed successfully
```

4\. Click Save.

This verifies that Java is available to the Jenkins build process.

### Step 10: Configure Slack Notifications

![Deploy-a-Java-Web-Application-to-Tomcat-Server-Using-Jenkins-with-Slack-Notification.md · GitHub](https://images.openai.com/static-rsc-4/iJbZr5ZCFOi3LTQxnSNeGDB6fy-xEGrSyIAkK4987ipTpqbjmpS42Zxtcj6t2I4L1Qm3v0OPPPUnv-T9iUm-gJV9KeyqBY2O7HT2SWAUpknTUnQoAEu9g6AyvWZm00gbXH6dvbyvTRMryJfaJrkDHwBL0Ccj2vQVnFIok_5NC8hbqj3K4lRQBa6oQoqgtCm6?purpose=fullsize)

* Open your `demo123` project.

* Click Configure.

* Scroll down to Post-build Actions.

* Click Add post-build action.

* Select Slack Notifications.

Enable the available notification options:

* Notify Success

* Notify Failure

* Notify Unstable Build

6\. Click Save.

### Part 4 – Execute and verify

### Step 11: Build the project

![How to Install Jenkins on Ubuntu 22.04](https://images.openai.com/static-rsc-4/E6zaHuzqGye5CXnsX8LJvm6F1XMs4iy1L9NyI8at3NEtxHMbJeEdA3NGGsG7JGoMjIciq7Nu6uDxfBtvSf19fhXEj8jxQpLLNYTK6fqxfh8fUoJuDQnHiXr3F-89v_PQpFznFqWsYTDC0E4zxNid_KvTyjMP2AlUq-MYmanpOVyCJOnu4HFuuS8YhJlpF-M5?purpose=fullsize)

* Open `demo123`.

* Click Build Now.

* Wait for the build to finish.

* Open the latest build.

* Click Console Output.

Expected output:

```text
java version information

Jenkins build executed successfully

Finished: SUCCESS
```

### Step 12: Verify Slack notification

* Go back to Slack.

* Open channel `demo-1`.

* Check whether Jenkins has sent a build notification.

Expected result:

```text
Jenkins Build Notification

Project: demo123
Build Status: SUCCESS
Build Number: 1
```

The exact message format may differ.

Your notebook's final step is:

Slack → Home → Green notification line → Integrated Successfully.

### Complete experiment workflow for your record

* Login to Slack and create workspace.

* Create public channel `demo-1`.

* Search Jenkins CI under Slack Apps.

* Add Jenkins CI to Slack and select channel.

* Copy Slack integration token.

* Install Slack Notification plugin in Jenkins.

* Configure Jenkins System settings.

* Add Slack token under Global Credentials as Secret text.

* Test connection and save.

* Create Freestyle Project `demo123`.

* Add Windows batch build step.

* Configure Slack Notifications under Post-build Actions.

* Save and click Build Now.

* Verify successful notification in Slack.

Result: Jenkins was successfully integrated with Slack to send automated build notifications.

### Common problems

| Problem                | What to check                |
| ---------------------- | ---------------------------- |
| Test connection failed | Token and workspace name     |
| No Slack message       | Bot membership and channel   |
| Plugin not visible     | Plugin installation          |
| Build failed           | Console Output               |
| Authentication error   | Token type and configuration |

One important practical tip: Your notebook follows the older Jenkins CI integration-token workflow. If the current Slack interface offers only the newer bot-token workflow, use the modern configuration rather than trying to force the old token into it.

You now have the complete procedure for Experiment 5, in notebook order. 🔥

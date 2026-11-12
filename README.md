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

* Bro, we'll follow your notebook exactly in the same order, step by step, for the Jenkins–GitHub Webhook experiment.

### Experiment: Jenkins – Webhook

Objective: Automatically trigger a Jenkins pipeline whenever code is pushed to a GitHub repository.

### Step 1 — Download Cloudflared

![Expose local Web App to the internet with Cloudflare tunnels - DEV Community](https://images.openai.com/static-rsc-4/OIOAsXE5qujlKd1OVZAEsKFioPw54mEWCJfkqsHwFDoQ2cnDuPxmsAd39S7sc-WvopkD9HZKiY_zMs7QN7vNdc1vqUt5-6KKKcK3-WP-Ki_rgt44jwLzzb75fAoLZq_XRpg6nMIoXOE4GYXBQA-VmO3e31qJHlhJ97jurRNVQckcy782j-ugy8EtNBSrlvJ5?purpose=fullsize)

* Open the [Cloudflare download page](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/?utm_source=chatgpt.com).

* Download the Windows 64-bit version (`cloudflared-windows-amd64.exe`).

* Save it in your Downloads folder.

### Step 2 — Login to Jenkins

* Open Google Chrome.

* Enter:

`http://localhost:8080`

* Login using your Jenkins username and password.

* Keep Jenkins running.

### Step 3 — Login to GitHub

* Open [GitHub](https://github.com/?utm_source=chatgpt.com).

* Login to your GitHub account.

* Keep GitHub open.

### Step 4 — Open CMD and start Cloudflared

* Press `Windows + R`.

* Type `cmd` and press Enter.

* Execute these commands one by one:

Command 1:

```cmd
cd %USERPROFILE%\Downloads
```

Command 2:

```cmd
dir cloudflared*
```

Check whether the Cloudflared executable is present.

Command 3:

```cmd
cloudflared-windows-amd64.exe tunnel --url http://localhost:8080
```

* Wait for Cloudflared to start.

* You will see a URL similar to:

```text
https://random-name.trycloudflare.com
```

6\. Copy this URL and keep it safely.

Keep this CMD window open throughout the experiment. The URL is temporary and may change when you restart the tunnel.

### Step 5 — Create a new repository in GitHub

![Chapter 6 Git and GitHub | The Unix Workbench](https://images.openai.com/static-rsc-4/5N97Q396EVhUF9l_dYS87jeUSvSBcSmg0woEmloPZEOMdBlzl-EuVykr802DeNG3UQg_pafmqIz9HxY-6tbmZpLG3I7L-IAOPgd8oQyhXG-kKmdNuhw3OtWSa4Ba6MSscT873kwbfy8F4EBLZO4HxHSSQ_cMaM1hcDHfwIBBjo6v7nj5Voz4tLA7vAZ0u6FO?purpose=fullsize)

* Open GitHub.

* Click the `+` icon → New repository.

* Enter a repository name, for example:

`Jenkins-Webhook`

* Select Public or Private as instructed by your lab.

* Click Create repository.

* Add the following three files to the repository:

* `app.py`

* `test.py`

* `Jenkinsfile`

7\. Your notebook says to get these files from another repository. Use the files provided by your faculty or lab repository. Don't change their contents unnecessarily.

Check: All three files should be present in your GitHub repository.

### Step 6 — Create a Pipeline in Jenkins

![How to create a Jenkins Pipeline job - DEV Community](https://images.openai.com/static-rsc-4/3fSD9eZdnCtZxyVt8BwFnsbgnA4HaKrLcSd8NnBoVddoZefPsoDSSvbj1rubSKvsk6uKJ34Ef2EL4dV0cXNeSGIH9BxLcIULU72R5Y6JgEnTucAh2s_OH646D_UOo0YFhiSdSdvovSAUiwyFrnIRzPsgdMDS8rX491OR4CXZJVzPh174ujpkD0BjO31kbPKn?purpose=fullsize)

* Open Jenkins: `http://localhost:8080`

* Click New Item.

* Enter the item name:

`S1`

* Select Pipeline.

* Click OK.

Your pipeline job is now created.

### Step 7 — Configure GitHub Webhook

![The importance of verifying webhook signatures | Snyk](https://images.openai.com/static-rsc-4/IYBJeL_BRXXPPvWh4ZU1WPMr0zPn4TBgHTNpms7w0-TU6rUfQ7I5QdlqQQKYIS5J_BF9qNhVWcKIrQvNpjfQ7NSXlZ-IUvqhs_oc-bwCL9WcjqDleJGDizgJwHPWGByLYEUnHpVL1pI0i8-7aW21LdQuFn7V1I8cYh6YO7woqu__M2a3Mobt0yo1XxIrXdMH?purpose=fullsize)

Part A: Configure webhook in GitHub

* Open your GitHub repository.

* Click Settings.

* Select Webhooks from the left menu.

* Click Add webhook.

Fill in the following details:

| Field         | Value                                                 |
| ------------- | ----------------------------------------------------- |
| Payload URL   | Your Cloudflared URL + /github-webhook/               |
| Content type  | application/json                                      |
| Secret        | Leave blank for this lab, unless instructed otherwise |
| Which events? | Send me everything                                    |

Example:

```text
https://random-name.trycloudflare.com/github-webhook/
```

Remember to use your actual Cloudflared URL, not this example.

5\. Click Add webhook.

Part B: Configure Jenkins URL

* Go back to Jenkins.

* Open Manage Jenkins.

* Go to System.

* Find the Jenkins URL field.

* Paste your public Cloudflared base URL.

Example:

```text
https://random-name.trycloudflare.com/
```

6\. Click Save.

### Step 8 — Configure the Jenkins Pipeline

![Automating CI/CD and GitOps with Jenkins | Red Hat Developer](https://images.openai.com/static-rsc-4/q36HEW_NmgZGtjwoA3JuhAAK6p22fMmTjPM__bLXFAKOq3rJFHLXeCer3lZDxPqlJiD-TRb74IGFf3o9msczzB-ReeILpwAdpgZsX_Kz8xQImDWPLergWP3ztgcroCGnbbaOS0guk_0ScvhkEHTTxzwoomSXg-4JFuFfvis7KIoDggyjG-E0VHIpq5K-1Nun?purpose=fullsize)

* Go back to the Jenkins dashboard.

* Open your job `S1`.

* Click Configure.

Part A: Build Triggers

* Scroll down to Build Triggers.

* Select:

    `GitHub hook trigger for GITScm polling`

Part B: Pipeline

* Scroll down to the Pipeline section.

* Under Definition, select:

    `Pipeline script from SCM`

* Under SCM, select:

    `Git`

* Repository URL: Paste your GitHub repository URL.

    Example:

    ```text
    https://github.com/username/Jenkins-Webhook.git
    ```

* Branch Specifier:

    ```text
    */main
    ```

    Check your actual branch name in GitHub. If it is `master`, use `*/master`.

* Script Path:

    ```text
    Jenkinsfile
    ```

* Click Apply.

* Click Save.

### Step 9 — Test the Webhook

Now check whether everything is working.

* Open your GitHub repository.

* Open `app.py` or another file.

* Make a small change.

* Click Commit changes.

* Go back to Jenkins.

* Open the `S1` pipeline.

* Check Build History.

![](https://images.openai.com/static-rsc-4/87S1iJvCzk77L0JHRyKV8CB9er8OW70gAOSizjp9z2veEYfb6ONx8M9wTQmnsflKRbQtQIFLskSThWnLGB4_w60J49_IDVNBe0IDQs7p27M8DcdzW6auNUOIILC-9eWa3236RrPFzAcE6Qxa8n6V-fFhfBFardn9aGh7X_C8KmDRD6j_1MzXlOTJOIFBm5WC?purpose=fullsize)

Expected result

A new Jenkins build should automatically start after your GitHub commit.

You can also verify the webhook:

* GitHub → Repository → Settings → Webhooks.

* Click your webhook.

* Open Recent Deliveries.

* Check the latest delivery response.

A successful delivery generally returns HTTP 200.

### Final experiment checklist

Experiment progress

0/13

Download Cloudflared

Login to Jenkins

Login to GitHub

Run Cloudflared tunnel in CMD

Create GitHub repository

Upload app.py, test.py and Jenkinsfile

Create S1 Pipeline in Jenkins

Configure GitHub webhook

Configure Jenkins URL

Enable GitHub hook trigger

Configure Pipeline script from SCM

Apply and Save

Commit a change and verify automatic build

Important: Keep Jenkins running and the Cloudflared CMD window open while testing. Stop the tunnel after completing the experiment. Don't share the temporary public URL or Jenkins credentials.

Follow these steps in order, and don't skip ahead. If you get stuck at any step, send me a screenshot and I'll guide you from that exact screen.

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

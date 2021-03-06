<h1 align="center" style="border-bottom: none;"> Watson Assistant Chatbot for SAP Cloud Platform</h1>
<h3 align="center">This Node.js app demonstrates how easily a chatbot can be built that is running on the SAP Cloud Platform and that is leveraging the Watson Assistant service on the IBM Cloud.</h3>

The [assistant-simple](https://github.com/watson-developer-cloud/assistant-simple) was slightly modified so the Node.js app is deployed on the SCP. There's also a [demo][demo_url] of the original app - apps on SCP trial accounts are stopped after a certain time. Please note that both animations in this repo are still from the orginal IBM Cloud repo. This one shows the dialog.

![Demo](readme_images/demo.gif)

As both, IBM Cloud and SAP Cloud platform, have Cloud Foundry runtimes it was possible to deploy the assistant on the SAP Cloud Platform.

![Assistant on SAP Cloud Platform](readme_images/bank-assistant.jpg)

The solution demonstrates how simple it is to deploy Cloud Foundry applications on different platforms and how to consume services from other platforms via a REST API.

![architecture](readme_images/architecture.jpg)

Please note this app uses the [Watson Assistant V2 API](https://cloud.ibm.com/apidocs/assistant-v2#introduction). To access a version of the V1 app, you can go to [v1.4.1](https://github.com/watson-developer-cloud/assistant-simple/releases/tag/v1.4.1).

If you need more information about the V1 API, you can go to the [Watson Assistant V1 API page](https://cloud.ibm.com/apidocs/assistant#introduction).


## Prerequisites

It is assumed that you have an account on the SAP Cloud Platform and downloaded the [Cloud Foundry Command Line Interface](https://developers.sap.com/tutorials/cp-cf-download-cli.html).

1. Sign up for an [IBM Cloud account](https://cloud.ibm.com/registration/).
1. Download the [IBM Cloud CLI](https://cloud.ibm.com/docs/cli/index.html#overview).
1. Create an instance of the Watson Assistant service and get your credentials:
    - Go to the [Watson Assistant](https://cloud.ibm.com/catalog/services/conversation) page in the IBM Cloud Catalog.
    - Log in to your IBM Cloud account.
    - Click **Create**.
    - Click **Show** to view the service credentials.
    - Copy the `apikey` value, or copy the `username` and `password` values if your service instance doesn't provide an `apikey`.
    - Copy the `url` value.

## Configuring the application

1. In your IBM Cloud console, open the Watson Assistant service instance

2. Click the **Import workspace** icon in the Watson Assistant service tool. Specify the location of the workspace JSON file in your local copy of the app project:

    `<project_root>/training/bank_simple_workspace.json`

3. Select **Everything (Intents, Entities, and Dialog)** and then click **Import**. The car dashboard workspace is created.

4. Click the menu icon in the upper-right corner of the workspace tile, and then select **View details**.

5. Click the ![Copy](readme_images/copy_icon.png) icon to copy the workspace ID to the clipboard.

    ![Steps to get credentials](readme_images/assistant-simple.gif)

6. In the application folder, copy the *.env.example* file and create a file called *.env*

    ```
    cp .env.example .env
    ```

7. Open the *.env* file and add the service credentials that you obtained in the previous step. The Watson SDK automatically locates the correct environmental variables for either `username`, `password`, and `url` or the `apikey` and `url` credentials found in the *.env* file.

    Example *.env* file that configures the `apikey` and `url` for a Watson Assistant service instance hosted in the US East region:

    ```
    ASSISTANT_IAM_APIKEY=X4rbi8vwZmKpXfowaS3GAsA7vdy17Qhxxxxxxxx
    ASSISTANT_URL=https://gateway-wdc.watsonplatform.net/assistant/api
    ```

    - If your service instance uses `username` and `password` credentials, add the `ASSISTANT_USERNAME` and `ASSISTANT_PASSWORD` variables to the *.env* file.

    Example *.env* file that configures the `username`, `password`, and `url` for a Watson Assistant service instance hosted in the US South region:

    ```
    ASSISTANT_USERNAME=522be-7b41-ab44-dec3-xxxxxxxx
    ASSISTANT_PASSWORD=A4Z5BdGENxxxx
    ASSISTANT_URL=https://gateway.watsonplatform.net/assistant/api
    ```
    However, if your credentials contain an IAM API key, copy the `apikey` and `url` to the relevant fields.
    ```JSON
      {
        "apikey": "ca2905e6-7b5d-4408-9192-xxxxxxxx",
        "iam_apikey_description": "Auto generated apikey during resource-key ...",
        "iam_apikey_name": "auto-generated-apikey-62b71334-3ae3-4609-xxxxxxxx",
        "iam_role_crn": "crn:v1:bluemix:public:iam::::serviceRole:Manager",
        "iam_serviceid_crn": "crn:v1:bluemix:public:iam...",
        "url": "https://gateway-syd.watsonplatform.net/assistant/api"
      }
    ```
    ```
    ASSISTANT_IAM_APIKEY=ca2905e6-7b5d-4408-9192-xxxxxxxx
    ```

8. Add the `ASSISTANT_ID` to the previous properties

    ```
    ASSISTANT_ID=522be-7b41-ab44-dec3-xxxxxxxx
    ```

## Running locally

1. Install the dependencies

    ```
    npm install
    ```

1. Run the application

    ```
    npm start
    ```

1. View the application in a browser at `localhost:3000`

## Deploying to the SAP Cloud Platform

1. Select the correct [region](https://developers.sap.com/tutorials/cp-cf-download-cli.html) and log in
    ```
    cf api https://api.cf.eu10.hana.ondemand.com
    cf login
    ```
1. Edit the *manifest.yml* file. Change the **name** field to something unique.  
  For example, `- name: my-app-name`.
1. Deploy the application

    ```
    cf push
    ```

1. View the application online at the app URL.  
For example: https://my-app-name.cfapps.eu10.hana.ondemand.com


## License

This sample code is licensed under Apache 2.0.  
Full license text is available in [LICENSE](LICENSE).

## Open Source @ IBM

Find more open source projects on the
[IBM Github Page](http://ibm.github.io/).


[demo_url]: https://assistant-simple.ng.bluemix.net/
[Watson Assistant doc_intents]: https://cloud.ibm.com/docs/services/conversation/intents-entities.html#planning-your-entities
[Watson Assistant docs]: https://cloud.ibm.com/docs/services/assistant/index.html#index
[Watson Assistant docs_landing]: (https://cloud.ibm.com/docs/services/assistant/index.html#index)
[node_link]: (http://nodejs.org/)
[npm_link]: (https://www.npmjs.com/)
[sign_up]: https://cloud.ibm.com/registration

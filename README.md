# Get started with Cloud Foundry and IBM Whitewater

### Continuously deliver a Cloud Foundry app with IBM Whitewater GHE

![Toolchain image](.bluemix/toolchain.png)

This template will configure a toolchain that can:
* perform rolling deploys through Bluemix stage1 (YS1) and then to Bluemix prod (YP).
* provide cognitive insights to learn where you most need to improve your developer productivity, code quality, and delivery cycle times; as well as provide quality gates that will stop a deploy that doesn’t cut the mustard.
* track code deployments back to GHE commits and issues
* notify about delivery process in Slack
* allows to edit code online with WebIDE (but you can use desktop tools at your preference)
* enable the required 
runtime libraries for the Watson Cloud Engineering Service Contract

### To get started, click **Create toolchain**.

[![Deploy To Bluemix](https://console.ng.bluemix.net/devops/graphics/create_toolchain_button.png)](https://console.ng.bluemix.net/devops/setup/deploy/?repository=https%3A//github.com/open-toolchain/cf-starter-wwghe-toolchain)

---
### Learn more

* [Step by step tutorial]() -- coming soon
* Learn about [Whitewater](https://whitewater.ibm.com)
* [Getting started](https://bluemix.net/devops)
* [Documentation](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/index.html?pos=2)
* [Toolchains on the Bluemix Garage Method site](https://www.ibm.com/devops/method/category/tools)
* Blog: [Bluemix Continuous Delivery is now live](https://www.ibm.com/blogs/bluemix/2016/11/bluemix-continuous-delivery-is-now-live/)
* Video: [Introducing IBM Bluemix Continuous Delivery](https://www.youtube.com/watch?v=QPSAZ64APpc&feature=youtu.be) (2m12s)

---

## Working with the Runtime Libraries - Manifest Runtime

* Learn about the [Watson Cloud Engineering Playbook](https://pages.github.ibm.com/the-playbook/index.html)
* Learn about the [Service Contract](https://pages.github.ibm.com/CloudEngineering/service_contract/)

### How the integration works

The Cloud Engineering Guild provides a set of runtime libraries that are used to verify that the different elements in the Service Contract are in place.

This integration is added to your toolchain and enabled in your application as follows:

#### Manifest Runtime Libraries
* A second pipeline is created to add, in a new branch, the required libraries to your repository.
    > Note that the pipeline must be run manually.  You can change this to run automatically if needed however you will need to merget he changes to the `master` branch before they are enabled for your application.

* The runtime manifest template is generated and customized for your application
* All the changes are added as a new branch.  All you need to do is create and merge the pull request

#### Your application
After the new branch is merged, your application will now contain the following:
  * `manifest` directory with the required files
  * `libibmmanifest.tar.gz` which contains the compiled files
  * `.profile` used to enable the objects when your application is launched

Most of the properties usedin the mainifest are derived from your applicaton and toolchain names.  Those can be updated **before** creating your toolchain.  The property `REGION_ID` used in the `STAGING` and `PROD` stages of your pipeline needs to match the region your application is being deployed to.

#### Keeping the runtime libraries updated
Periodically, the Cloud Engineering Guild will update the runtime libraries and you will need to incorporate them into your build and deploy process.

You can run the `Manifest Runtime` pipeline to add the new changes to your repository.  Simply run the pipeline, create a pull request, and merge into your application.
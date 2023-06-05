
# Add JS and CSS reference on Modern Pages via SPFx application customizer extension

This repo is a react based SPFx web part and extension that allows users to add/modify/delete custom js and css file references using SPFx application customizer extension all modern pages within SP online site. This web part provides an interface to JS and CSS file references so that we don't have to modify code when we need to change references or add new references in the future. As part of security measures, this actions on web part can be only accessed by users who have Manage web permission on site.

Web Part in Action

![Web part in action](assets/webpartinaction.gif?raw=true "web part in action")

Challenges/Drawback with ONLY using SPFx extension for adding js and css file references.
* JS and CSS file references links needs to be hardcoded in solution
* Changes to code required if we need to change add new reference or remove existing reference.
* Redeployment of package and installation
* Different solution would be required for different site collections as we would definitely need different header js and css file references for each site collection(most of cases)
* High maintenance and time consuming for simple task. 

To overcome this drawbacks, this solution comes handy. This is reusable component which can be used by developers to eliminate creating Extension on their own. Feel free to connect on twitter:@siddh_me for any details.

### Features of solution

* Web part to configure JS and CSS file reference.
* Edit functionality if at least one JS or CSS reference is already added via this solution
* Completely remove all the references added via this solution
* Support for relative url also, if your js and css file is referred from some document library in same site collection.
Path can be `/sites/mysc/style library/js/custom.js` or `/sites/mysc/style library/css/custom.css`


## Compatibility

| :warning: Important          |
|:---------------------------|
| Every SPFx version is only compatible with specific version(s) of Node.js. In order to be able to build this sample, please ensure that the version of Node on your workstation matches one of the versions listed in this section. This sample will not work on a different version of Node.|
|Refer to <https://aka.ms/spfx-matrix> for more information on SPFx compatibility.   |

![SPFx 1.15.2](https://img.shields.io/badge/SPFx-1.15.2-green.svg) 
![Node.js v16 | v14 | v12](https://img.shields.io/badge/Node.js-v16%20%7C%20v14%20%7C%20v12-green.svg) 
![Compatible with SharePoint Online](https://img.shields.io/badge/SharePoint%20Online-Compatible-green.svg)
![Does not work with SharePoint 2019](https://img.shields.io/badge/SharePoint%20Server%202019-Incompatible-red.svg "SharePoint Server 2019 requires SPFx 1.4.1 or lower")
![Does not work with SharePoint 2016 (Feature Pack 2)](https://img.shields.io/badge/SharePoint%20Server%202016%20(Feature%20Pack%202)-Incompatible-red.svg "SharePoint Server 2016 Feature Pack 2 requires SPFx 1.1")
![Local Workbench Compatible](https://img.shields.io/badge/Local%20Workbench-Compatible-green.svg)
![Hosted Workbench Compatible](https://img.shields.io/badge/Hosted%20Workbench-Compatible-green.svg)
![Compatible with Remote Containers](https://img.shields.io/badge/Remote%20Containers-Compatible-green.svg)

## Applies to

* [SharePoint Framework](https://learn.microsoft.com/sharepoint/dev/spfx/sharepoint-framework-overview)
* [Office 365 tenant](https://learn.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant)

### Package and Deploy

 Try first on local work bench.

Change the `pageURL` property in `/config/serve.json` - This should be a valid modern page on your site collection.


```bash
git clone the repo
```
* From your command line, change your current directory to the directory containing this sample (`react-add-js-css-ref`, located under `samples`)

```bash
npm i
gulp serve
```
- Execute the following gulp task to bundle your solution. This executes a release build of your project by using a dynamic label as the host URL for your assets. This URL is automatically updated based on your tenant CDN settings:
```bash
gulp bundle --ship
```
- Execute the following task to package your solution. This creates an updated `webpart.sppkg` package on the `sharepoint/solution` folder.
```bash
gulp package-solution --ship
```
- Upload or drag and drop the newly created client-side solution package to the app catalog in your tenant.
- Based on your tenant settings, if you would not have CDN enabled in your tenant, and the `includeClientSideAssets` setting would be true in the `package-solution.json`, the loading URL for the assets would be dynamically updated and pointing directly to the `ClientSideAssets` folder located in the app catalog site collection.

### How to Use Solution

* Once app is deployed to app catalog successfully.
* Install app to required site collection
* Create new modern page. Add **addJsCssReference** web part to page. Publish the page.
* Use grid to add js and css file references, both are separate sections.
* On Success message - Refresh the page and you would see your js and css files will be loaded.
* To Edit/Remove, go to same page again and Use **Activate** or **Deactivate**.
* Only Users with Manage Web permission will be able to access web part and add/modify references.

### High level design of Solution

* SPFx solution with 2 components 1. SPFx Web part 2. SPFx Extension Application Customizer
* Disables Automatic activation of SPFx extension when app is installed.
* React based solution
* Register Custom action with ClientSideComponentId of Extension component
* Passes parameters to Extension with ClientSideComponentProperties











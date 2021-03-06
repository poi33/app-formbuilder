# Enonic XP Form Builder

This is an application that lets you build simple web forms in Enonic XP. It can send data by e-mail and/or store data in Enonic for later report running with the included Form Report widget. Reports are stored as a Comma-Separated Values (CSV) file which is viewable in your spreadsheet application of choice. The feature set is relatively close to the built-in form builder that was in Enonic CMS, but with added user-friendliness using features in Enonic XP. With regards to how personal data is processed, the app is configurable at several different security levels and with default options that erase stored personal data once they have been used by the system, in order to be GDPR compliant.

The app was originally a fork of [XP Form Builder by Vegard Haugstvedt](https://github.com/it-vegard/xp-form-builder) with the original artwork and parts of that data model still present in the code. The main difference that this app has a closer resemblance to the form builder that was in Enonic CMS.

## Installation

There are three options:

* First option is to open the Enonic XP Applications admin tool. In here select "Install" and find this app in the Market list of available apps.
* Second alternative is to simply download the app [JAR file](http://repo.enonic.com/public/com/enonic/app/formbuilder/1.0.0/app-formbuilder-1.0.0.jar) and move it to the XP installation's `$XP_HOME/deploy` folder.
* Or you can build this app with gradle. First, download the zip file of this repo. Unpack it locally. In the terminal, from the root of the project, type `./gradlew build`. On Windows, just type `gradlew build`. Next, move the JAR file from `build/libs` to your `$XP_HOME/deploy` directory. The Form Buider app will now be available to add to your websites through the Content Studio admin tool in Enonic XP.

If you are upgrading to a newer version of this app by any other means than the Applications admin tool described above, make sure to remove the old version's JAR file from the `$XP_HOME/deploy` directory.

From the Content Studio: Edit your site and add the application. Save. You may notice that the application is highlighted, because required fields have not been filled out. These are the fields described in the section directly below.

## Application setup and configuration options

### E-mail FROM address

**Required.** Although the Form Builder app can store form responses in Enonic without sending data by e-mail, this configuration field has been set to required since some specific setup choices depend on it.

### User-submitted data: Storage location and access policy

**Required.** This sets the policy for how and where data is stored, if at all. The setting may be changed later without losing any data, but then data will reside in different locations before and after the change.

* If "Minimal" is selected, each form *must* have a working e-mail address to send the data to, or else data will be lost if the e-mail isn't sent, since the data is not stored in Enonic.
* "Regular" will store the form response data in a hidden repo and enable running reports with the Form Report widget. This is the default setting and is a nice compromise between the need for data management/security and ensuring that personal data rights are protected.
* "Full" is like "Regular", but stores the form responses directly as content in Content Studio. This provides the most control over the data (for example when fullfilling a GDPR "Right to erasure" request) but might fill up Content Studio with thousands of form submissions if a form is popular and the submissions are not removed periodically.

### reCAPTCHA v2 (anti-spam measure)

Are you a robot? To enable reCAPTCHA, both the Site Key and and Secret Key fields must be filled out. Create and administrate your Google v2 reCAPTCHA API keys here: https://www.google.com/recaptcha/admin

## Create a page template to show your forms

1. From the Content Studio: Create a page template. You can choose to base this on existing page templates, or choose the one supplied with this app.
2. Set what content types to associate the template with. You can of course associate it with the Form content type, which will create standalone form pages, or you can add the form part on a landing page or similar if the form is just to be a minor part of the page.
3. From the page editor: Add the "Form view" part. If you only associate the template with the Form content type: Save and start making forms. If adding forms on other pages: You will have to edit the part configuration on the pages you want to show a form. In the part configuration you add the form you want to display. This also works if you make a fragment of the form, so the form is shown on any page you add the fragment.

## Creating your first form

From the Content Studio: Create a new content of type "Form" somewhere on a site where you added the application. If you made a page template that supports the Form content type, otherwise you must add it to a page using the "Form view" part.

You have many options on how to configure your form, but in many cases you can just leave the default settings in place. The only part you need to do, is add one or more input fields. **NB:** If you've configured the app to use the "Minimal" data storage policy, you also *must* add one or more "Send to" e-mail addresses in the corresponding field further down.

## Form Report widget

If the Form Builder app has been configured to store data using the "Regular" or "Full" policy, form responses are stored as "base:unstructured" content, together with any file attachments that users have submitted in File inputs in the web form. These may then be exported to a Comma-Separated Values (CSV) file which is viewable in your spreadsheet application of choice.

### Automatic form response deletion upon running reports

By default, a checkbox "Delete the exported form responses" inside the widget is selected. This deletes all the form responses that were included in your report as soon as the report has been generated. This is in order to comply with general data protection regulation. If for some reason you need to keep the data stored in Enonic XP after running your report (such as for testing purposes), you need to *uncheck* this checkbox.

### Other data access options

If you need access to form response data at a more individual level without running reports at regular intervals, there are options provided with other Enonic XP apps:

* Using the widget available in the Content Viewer app (requires the data storage policy set to "Full").
* Using the admin tool available in the Data Toolbox app. This also allows individual removal of form response data for both data storage policies "Regular" and "Full".

## Development instructions

### Prerequisites
* Install Enonic XP 6.13.0 or above
* Set the XP_HOME variable to point to your Enonic home folder.

### Deployment
* Run "./gradlew deploy" (UNIX) or "gradlew.bat deploy" (Windows) to install to a local installation.

## Releases and Compatibility

| Version        | XP version |
| ------------- | ------------- |
| 1.0.0 | 6.13.0 |

**Important!** This App is not backwards compatible with any XP version before 6.13.

## Changelog

### Version 1.0.0

* First release

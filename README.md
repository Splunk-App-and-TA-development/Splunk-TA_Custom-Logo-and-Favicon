# splunk TA for Custom Logo and Favicon
Technical add-on to provide custom Logos and Favicons for the Search Heads Frontend pages and Logo for Reports.
This technical addon can then be installed to all your Splunk Servers to have a standartisized setup.

## Installation and configuration
1. Download the TA from splunkbase.com or Github.

2. Install the TA **Splunk-TA_Custom-Logo-and-Favicon** to `/opt/splunk/etc/apps/` on one of your Search Heads.
_After the installation you need to adapt some settings before restart Splunk._

3. Upload your dedicated **favicon.ico** in to `appserver/static/customfavicon`.
_There are a lot of online possibilities to create your own favicon. For example: https://www.favicongenerator.com/._

4. Edit the custom background image **background-splunk-generic-company-logo_1920x1200.png** stored in `appserver\static\logincustombg` and change it according to your Company logo, etc...
	- Upload the new background image file back to the `appserver\static\logincustombg` folder.
	- Depending on your standard screen resolution you may need to change the image size (eg. 1920x1200 or 1024x640, etc ...)
	- The fastest way to edit the graphics it is by using paint.net. Download it under https://www.getpaint.net/download.html
	
5. Edit the custom background image **splunk-company-logo-red.png** stored in `appserver\static\logincustomlogo` and change it according to your Company logo, etc...
	- Upload the new Loginpage Logo file back to the `appserver\static\logincustomlogo` folder.
	- The fastest way to edit the graphics it is by using paint.net. Download it under https://www.getpaint.net/download.html

6. Edit the custom background image **logo-standard.png** stored in `appserver\static\logincustompdf` and change it according to your Company logo, etc...
	- Upload the new PDF Logo image file back to the `appserver\static\logincustompdf` folder.
	- The fastest way to edit the graphics it is by using paint.net. Download it under https://www.getpaint.net/download.html

7. Restart your Splunk Server: `/opt/splunk/bin/splunk restart`

### Components of the TA
The TA should be configured with the following configuration files:
- `alert_actions.conf`
- `web.conf`

Logos and Graphics stored in `appserver/static` folder
- Dedicated Favicon
- Login page Background image
- Login page company Logo
- PDF Company logo 


### Configuration

#### Login Page configuration

> Note: The app in this repo comes pre-configured with files in `local/`. The version on SplunkBase **is not preconfigured**, and requires the following manual steps.  
You can use local/*.conf files in this repo as templates to cofngiure the app in your environment.

```conf
[settings]
### Customization Frontend Graphs
loginBackgroundImageOption = custom
loginCustomBackgroundImage = Splunk-TA_Custom-Logo-and-Favicon:logincustombg/background-splunk-generic-company-logo_1920x1200.png

### Customization Frontend Logo
loginCustomLogo = Splunk-TA_Custom-Logo-and-Favicon:logincustomlogo/splunk-company-powered-logo-red.png

### Customization Frontend Favicons
customFavicon = Splunk-TA_Custom-Logo-and-Favicon:customfavicon/favicon.ico

### Custom Footer for Embeded PDF
embed_footer = <div class="footer"; align="center">Copyright <b>&copy;</b> 2017-2021 by YOUR COMPANY - all rights reserved.<br>Find us under <a href="https://WWW-YOUR-COMPANY.COM"><img src="/static/app/TA-SRG_Custom-Logo-and-Favicon/company-logo/company-logo.png" title="https://WWW-YOUR-COMPANY.COM" width="49" height="17"/></a></div>

### Custom Login Page Footer
loginFooterOption = custom
loginFooterText = <div class="footer"; align="center">Copyright <b>&copy;</b> 2017-2021 by YOUR COMPANY - all rights reserved.<br>Find us under <a href="https://WWW-YOUR-COMPANY.COM"><img src="/static/app/TA-SRG_Custom-Logo-and-Favicon/company-logo/company-logo.png" title="https://WWW-YOUR-COMPANY.COM" width="49" height="17"/></a></div>

## Page Title Option
loginDocumentTitleOption = custom
loginDocumentTitleText = <YOUR-COMPANY> Security Splunk
```

#### PDF Page configuration

By default, Splunk logs changes in the `$SPLUNK_HOME/etc/` directory every 10 minutes. In some cases, it may be desirable to do this more frequently, to ensure that no filechanges are missed. If this is desired, add the following to local/inputs.conf:

```conf
### PDF Logo Settings
pdf.logo_path = Splunk-TA_Custom-Logo-and-Favicon:logincustompdf/logo-standard.png

### PDF Mailsender Settings
from = <your-team-email-address>
mailserver = <your-smtprelay-server>
use_tls = 1

### PDF Disclamer Settings
footer.text = -<< <your-company-name> Enterprise Security SIEM Disclamer >>-\
\
Please, DO NOT REPLY !\
 \
As SIEM operators, we take the protection of personal information seriously.\
We treat personal information as confidential and will handle it in accordance with data protection legislation as well as with the terms of this statement.\
\
Any files/attachments transmitted with this eMail are strictly confidential and are intended solely for the use of the individual or entity to whom they are addressed.\
\
If this message has been sent to you in error, you must not copy, distribute or disclose of the information it contains.\
Please notify the <your-company-team-name> Team immediately and delete the message from your system.\
\
Thank you for your understanding.\
For any questions, please contact us at <your-team-email-address>\
\
Kind Regards \
<your-company-team-name> Team\
\
+-+-+-+-+-+-+-+-+-+-+-+-+\
<your-company-name>\
<your-company-address>\
<your-company-po-box> <your-company-city>\
Phone <your-company-phone>\
<your-team-email-address>\
<your-company-web-url>\
+-+-+-+-+-+-+-+-+-+-+-+-+
```


### Deploy to other servers
Once you defined a standard for your Frontend page and PDF printout, you can save the TA locally to your client and install it on all your other servers.
If you manage your servers via a deployment server, then deploy the TA via it.

## Who is this app for?
This TA is used to provide a standartisised Login page as well as standartisised PDF template and Mail footer.

## How does the app work?
This ta provides configuration standards and graphics for the Login page, PDF template and Mail template. 

## **Release Notes**

#### v 1.0.1
- Added generic graphics for the initial installation
- Updated Manuals to explain how to adapt the graphics and configuration files

#### v 1.0.0
-Initial Versionsion


## **Support**
Support is not guaranteed and will be provided on a best effort basis.
Please use Github to open issues or feature requests:
- **https://github.com/Splunk-App-and-TA-development/Splunk-TA_Custom-Logo-and-Favicon/issues**


#### Splunk Version Support

| Supported Splunk Versions  | Unsupported or Deprecated  |
| --- | --- |
|  8.2.x, 8.1.x, 8.0.x, 7.3.9, 7.3.6 | 7.3.5 and lower, 6.6.x, 6.5.x, 6.4, 6.3, 6.2, older  |


#### Credits
This app is supported by Patrick Vanreck (SwissTXT). Contact us under: **[yoyonet-info@gmx.net](mailto:yoyonet-info@gmx.net)**.

- Find us under **[SECLAB Splunk App & TA Development](https://github.com/Splunk-App-and-TA-development "SECLAB Splunk App & TA Development")**
- Send questions to ***[yoyonet-info@gmx.net](mailto:yoyonet-info@gmx.net)***
- Developped by **Patrick Vanreck**


#### Software License
Please find the license for this software here: https://github.com/Splunk-App-and-TA-development/Splunk-TA_Custom-Logo-and-Favicon/master/LICENSE


#### Copyrights
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"),<br>
to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense,<br>
and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
	
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.


<div class="footer">
    Copyright &copy; 2017-2021 by SwissTXT Security
</div>
# splunk TA for Custom Logo and Favicon

Technical add-on to provide custom Logos and Favicons for the Search Heads Frontend pages and Logo for Reports.

## Installation and configuration
Underhalf the Git repo you'll find two main folders that you need to upload to `/opt/splunk/etc/apps/`.
After the installation of booth folders in `/opt/splunk/etc/apps/` restart the Splunk daemon to make it run.

1. Create an new index in your environment: `index = splunk_confchange`

2. Upload the App **STXT-App_Confversion** to `/opt/splunk/etc/apps/`.
_App with the views of the Configuration Changes on your Splunk Servers._

3. Upload the TA  **TA-SRG_Confversion** `/opt/splunk/etc/apps/`.
_TA with the extractions and parsings of the Configuration Changes on your Splunk Servers._

4. Restart your Splunk Server: `/opt/splunk/bin/splunk restart`

### Splunk Components

The **TA-SRG_Confversion** can be installed on all Splunk components including Universal Forwarders. This TA should be installed and configured on all components where configuration change tracking is desired.

The **TA-SRG_Confversion** must be installed on Indexers and intermediate HFs, as it contains index-time transforms. 

The **TA-SRG_Confversion** must be installed on Search Heads, as it comes bundled with important KOs for viewing the indexed configuration data. 

The **STXT-App_Confversion** should be installed on your DMC Console of the Splunk Search Head where the DMC Console is installed to see all Changes on all your servers.

### Configuration

> Note: The app in this repo comes pre-configured with files in `local/`. The version on SplunkBase **is not preconfigured**, and requires the following manual steps.  
You can use local/*.conf files in this repo as templates to cofngiure the app in your environment.

Create an index (local/indexes.conf) if you do not wish to ingest these logs into main. (recommended)

Create local/macros.conf and override the `conf_files_index` to point at the index you chose in the step above. 

Create local/inputs.conf to designate the index and enable the inputs. 

#### File change monitor polling interval

By default, Splunk logs changes in the `$SPLUNK_HOME/etc/` directory every 10 minutes. In some cases, it may be desirable to do this more frequently, to ensure that no filechanges are missed. If this is desired, add the following to local/inputs.conf:
```conf
[fschange:$SPLUNK_HOME/etc]
#poll every 30 seconds
pollPeriod = 30
```

This change can cause added load on the system. Ensure you are comfortable with that before implementing this change. 

### Security

This TA exposes potentially sensitive information to users. This includes any passwords/tokens/usernames contained within conf files on the instance. 

It is highly recommended that the index this TA uses be made accessible soley to administrators to prevent information disclousre to unauthorised parties. 

### Configuration Files Contained Within the Add-on
- app.conf
- indexes.conf
- inputs.conf
- props.conf
- transforms.conf




## Who is this app for?
This app is for anyone who wants to display several metrics on a small area of a dashboard.

## How does the app work?
This app provides a visualization that you can use in your own apps and dashboards.

To use it in your dashboards, simply install the app, and create a search that provides the values you want to display.


## Development
Please track issues here, on Github. Merge requests are welcome, but may not be addressed immediately. 

### v 1.0.0
-Initial version

# Support

Support will be provided by the developers on a best-effort basis. The developers make no commitment to continued development. The software is provided as is, and the developer accepts no responsibility for any issues with the software, or which may result as a consequence of using the software to the fullest extent permissible by the law.

Please find the license for this software here: https://github.com/Splunk-App-and-TA-development/Splunk-TA_Custom-Logo-and-Favicon/master/LICENSE


## Issues and Limitations
No kown limitations for the Use on Splunk Servers.

### Splunk Version Support
8.2.x, 8.1.x. 8.0.x, 7.x, 6.x


## Privacy and Legal
No personally identifiable information is logged or obtained in any way through this visualizaton.

## For support
Send email to yoyonet-info@gmx.net

Support is not guaranteed and will be provided on a best effort basis.
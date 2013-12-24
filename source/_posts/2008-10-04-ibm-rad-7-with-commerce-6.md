---
layout: post
title: Using IBM Rational Version 7.0 IDE
tagline: with IBM WebSphere Commerce Developer 6.0
date: 2008-10-04 13:10:00+00:00
tags: [ibm, websphere, commerce, rational, eclipse, ide]
category: development
comments: false
---
**(Note: This technique is NOT supported by IBM)** IBM's Rational family of IDE's (integrated development environments) are based on the Eclipse<a name='sdendnote1anc' href='#sdendnote1sym'><sup>1</sup></a> platform. IBM WebSphere Commerce Developer 6.0<a name='sdendnote2anc' href='#sdendnote2sym'><sup>2</sup></a> is one member of the family that is based on the Rational Application Developer 6.0<a name='sdendnote3anc' href='#sdendnote3sym'><sup>3</sup></a> and the WebSphere Application Server 6.0<a name='sdendnote4anc' href='#sdendnote4sym'><sup>4</sup></a>.

<!-- more -->

Rational Application Developer 7.0.x (RAD7) and other members of this family are based on an architecture that is significantly different from the Rational 6.0.x (RAD6) family. Since it is based on Eclipse 3.2.1 and can re-use existing Eclipse installations, many developers are finding that using RAD7 enhances productivity and allows the use and update of non-IBM Eclipse plug-ins as well using new Eclipse features.

**Note: This process has been tested with RAD and RSA (Rational Software Architect)**

The Commerce Developer environment can be created inside RAD7, with little or no limitation to functionality. There are two ways to do this:
1. Keep both RAD6 and RAD7 (easiest)
2. Use RAD7 only (requires modifications to Commerce Toolkit batch files and setup process).

For a detailed <a href='#analysis'>analysis</a>, read the analysis section below.

<a name='rad7withcommerce6'>&nbsp;</a>

##Quick Steps (keep both RAD6 and RAD7)
1. Make sure you have a working Commerce Development environment with RAD6.
2. Backup the `TOOLKIT\workspace` into a zip file and call it `workspaceRAD6.zip`
3. Open `RAD6_HOME\runtimes\base_v6\properties\profileRegistry.xml`. Find the entry for your WAS/WC profile, for example:
`<profile isDefault="false" name="WCTOOL~2_135924" path="C:\IBM\WCTOOL~2\wasprofile" template="C:\IBM\Rational\SDP\6.0\runtimes\base_v6\profiletemplates\default"/>`
4. Open `RAD7_HOME\runtime\base_v6\runtimes\profileRegistry.xml`. Copy the entry from above and update the template path to RAD7. Save the file. 
5. Start RAD7 and point it to the workspace folder.
6. Automatic migration will start – do NOT interrupt it – go into the Window->Preferences->Validation Dialog, and remove HTML, JSP and XML validation.
7. After migration completes, if any of the Commerce projects shows errors, correct them. If the errors are just JSP, HTML or XML errors that were flagged before the validators could be turned off, then just clean the projects (Project->Clean).
8. Two simple WebSphere servers will have been created (6.0 and 6.1) and Commerce Server will not be present. Create a new server:<br/>
![]({{site.url}}/assets/2008/CreateServer.jpg)
9. Pickup the configuration from the drop-down:<br/>
![]({{site.url}}/assets/2008/PickupConfig.jpg)
10. Add the Commerce EAR, Next, Next and Finish: <br/>
![]({{site.url}}/assets/2008/AddCommerceApp.jpg)
11. Open the server description, change and save (make sure to turn UTC off).  Also make sure that Automatic Publishing is turned off (will save a lot of time): <br/>
![]({{site.url}}/assets/2008/RenameServer.jpg)
12. **THIS STEP MAY or MAY NOT BE REQUIRED - only DO if the SERVER cannot find your PROJECTS in the workspace** : Copy the `looseconfigurations` folder to a new location :
<br/>FROM:`TOOLKIT\workspace\.metadata\.plugins\com.ibm.wtp.j2ee\looseconfigurations`
<br/>TO:`TOOLKIT\workspace\.metadata\.plugins\com.ibm.etools.wrd.websphere.v6\looseconfigurations`
13. Start the server and everything should be fine.

**NOTE:** If you plan to perform any automated workspace modifications like SETUP.BAT, or apply FIXPACKS that do the same, you will have to backup/delete or rename the RAD7 workspace, unzip the backed up RAD6 workspace and then run the modification. Afterwards, you should repeat the above steps again.

##Complex Method (using RAD7 only)
1. Make sure you have a working Commerce Development environment with RAD6. Makes sure you devise a backup scheme for all the changes here:
2. Backup the `TOOLKIT\workspace` into a zip file and call it `workspaceRAD6.zip`
3. Delete folder `TOOLKIT\workspace\.metadata`
4. Backup and delete folder `TOOLKIT\wasprofile`
5. Change `setenv.bat` to point to RAD7 home folder: `RAD_HOME` variable
6. In the `TOOLKIT\bin` folder, search and change all instances of `%RAD_HOME%\eclipse\jre\bin\java` to `%RAD_HOME%\jdk\jre\bin\java`
7. Change `setup.bat` to comment out the call to `setupPlugins.bat`
8. In `TOOLKIT\setup\setup.xml`, comment out the following elements: `<importPreferences . . . . />, <validationPreference . . . />, <ejbDeploy . . ./>, and <configureServer . . . .>`
9. Run setup.bat – it will fail towards the end, do not worry.
10. Follow all the instructions in the <a href='#rad7withcommerce6'>Quick Steps</a> method above. Before starting the server, run setdbtype.bat to move to DB2.
11. Import your non-IBM-provided projects into the workspace.

<a name='analysis'>&nbsp;</a>
##Analysis

To support development in RAD, the Commerce toolkit provides a workspace, batch files for workspace manipulation, and RAD Plug-ins.

**Plug-ins:** None of the toolkit-provided plug-ins is absolutely required. Here is a summary:
1. Documentation plug-ins: These can be unzipped and put into RAD7 in the SDP70\plugins folder, and they work fine.
2. ITLM plug-in: Do not install this as it conflicts with RAD fixpack 7.0.0.1
3. Optimistic Locking UI plug-in: This seems to work in RAD 7, but I have never had the opportunity to use it.
4. CommerceToolkitPlugin and ToolkitFeature: These contain ANT tasks that are implemented as Eclipse plug-ins in order to take advantage of certain Eclipse server features and to include the tasks in the exported ANT tasks list. We commented out these tasks in Step 8 of the Complex method above. Parts of these plug-ins can be used after tweaking the 'requires' section of the plugin.xml. The server part is known to not work as it works with the IBM server plug-ins and not the new Eclipse server support framework.

**Flow of setup.bat and setup.xml ANT build script:** Import plug-ins into the workspace, import the projects and setup workspace preferences (most of which are obsolete in RAD7). Create a WAS profile, and import it into the workspace, and set certain properties of the newly-created server. Then publish the WC application. You can now see easily how these steps correspond to the steps above.

**WebSphere version:** The runtime WebSphere 6.0 version that comes with RAD7 is above 6.0.2.11. This level is supported for Commerce but with certain patches. Please read the relevant IBM-supplied tech notes and documents.

<p><a name='sdendnote1sym' href='#sdendnote1anc'>1</a>&nbsp;http://www.eclipse.org</p>
<p><a name='sdendnote2sym' href='#sdendnote2anc'>2</a>&nbsp;http://www.ibm.com/software/genservers/commerce/commercestudio/</p>
<p><a name='sdendnote3sym' href='#sdendnote3anc'>3</a>&nbsp;http://www.ibm.com/software/awdtools/developer/application/index.html</p>
<p><a name='sdendnote4sym' href='#sdendnote4anc'>4</a>&nbsp;http://www.ibm.com/software/webservers/appserv/was/</p>


# ARM Discourse LDAP Plugin

This plugin was forked from the original discourse-ldap-auth plugin in order to customize
the login page.  Note that the html for the login page is part of the omniauth gem,
so we can't customize it easily.  So for now we are providing login page customizations
via css styles only.

That means that we have to add custom html as an svg background image :(

## Repo URL
The forked repo can be found here:
https://github.com/clansing/discourse-ldap-auth

## Editing the login page
Edit the ```css/form.css``` file to change the content of the login page.  Specifically, any 
additional html text is provided in the form::before and form::after styles as svg background images.

For example
```css
form::before {
    content: url("data:image/svg+xml;charset=utf8,%3Csvg xmlns='http://www.w3.org/2000/svg' width='650px' height='230px'%3E%3CforeignObject width='100%25' height='100%25'%3E%3Cdiv xmlns='http://www.w3.org/1999/xhtml' style='font-family: Helvetica; font-size: 12px; width: 100%25;'%3E%3Cdiv style='padding: 10px; border: 1px solid rgb(220, 220, 220); border-radius: 5px; background-color:rgb(245, 245, 245)'%3E This is a Department of Energy (DOE) computer system. DOE computer systems are provided for the processing of official U.S. Government information only. All data contained within DOE computer systems is owned by the DOE, and may be audited, intercepted, recorded, read, copied, or captured in any manner and disclosed in any manner, by authorized personnel. THERE IS NO RIGHT OF PRIVACY IN THIS SYSTEM. System personnel may disclose any potential evidence of crime found on DOE computer systems to appropriate authorities. %3Cp%3EUSE OF THIS SYSTEM BY ANY USER, AUTHORIZED OR UNAUTHORIZED, CONSTITUTES CONSENT TO THIS AUDITING, INTERCEPTION, RECORDING, READING, COPYING, CAPTURING, and DISCLOSURE OF COMPUTER ACTIVITY.%3C/p%3E%3C/div%3E%3Cdiv style='margin-top: 30px;'%3E%3Cdiv style='font-weight: bold; font-size: 14px;'%3E Please log in with your ARM LDAP account* credentials: %3C/div%3E%3Cdiv style='font-style: italic; margin-top: 5px;'%3E (Note that the first time logging into the forum, users will also need to be admitted by a site moderator.) %3C/div%3E%3C/div%3E%3C/div%3E%3C/foreignObject%3E%3C/svg%3E");
}
```

## Making the SVG URL

1. Open the ```css/svg-content.html``` page
2. Edit the ```<svg>``` element in either the ```<!--- FORM BEFORE -->``` or ```<!--- FORM AFTER -->```  section.
3. Open the SVG URL encoder at https://yoksel.github.io/url-encoder/
4. Paste the entire  ```<svg>``` element into the "Insert SVG:" box
5. Copy the text from the "Take Encoded:" box
6. Open the ```css/form.css``` file
7. Edit the ```form::before``` or ```form::after``` content attribute, depending upon which one you are modifying.
8. Paste the content from the "Take Encoded:" box into the content url at this location:
    ```css
    content: url("data:image/svg+xml;charset=utf8,PASTE_SVG_HERE");
    ```

See this discussion for  more info on using svg images to render html (there are some limitations):

https://stackoverflow.com/questions/32870788/css-using-raw-svg-in-the-url-parameter-of-a-background-image-in-ie

## How is this plugin added to Discourse?
1. ssh to discourse.adc.arm.gov using the cert you got from Pete
2. Follow these instructions: https://meta.discourse.org/t/install-plugins-in-discourse/19157

## How to redploy this plugin on the server
1. ssh to discourse.adc.arm.gov using the cert you got from Pete
2. Run these commands
   ```bash
   sudo bash
   cd /var/discourse
   ./launcher rebuild app
   ```
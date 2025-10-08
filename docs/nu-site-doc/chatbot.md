# Chatbot

**www** and **info** offer site visitors a chatbot on the front end.

As of Dec 2022 we are currently using **TWO** different chatbot providers. The floating 'chat' icon triggers a menu, which allows the user to select which chat option they want.

The code for all chatbot-related code is within our **nuedu-core-functionality** plugin: `plugins/nuedu-core-functionality/inc/chat`

Within this folder, the 'views' folder contains the actual front-end output of everything that lives on our end (floating chat icon, popup menu buttons). The actual chatbox popups are implemented via third-party services and we have limited control over their customization.

## Livechat

Livechat is our legacy chat solution which offers real-time chat with a live enrollment advisor. This runs through a third-party service called 'livechat'. Integration info can be set via wp-admin: **Customizer -> Web Services Integration -> Livechat**.

External platform site: [livechatinc.com](https://www.livechatinc.com) -- **unclear if we have a login or if this is managed by someone else.**

## NU-ton

NU-ton is a new Salesforce-backed "AI" chatbot. The implementation occurs via a code snippet that is provided to us by the Salesfore team, however we modify this snippet to suit our needs.

Configuration info (including code snippet) can be set via wp-admin: 'Chatbox' top-level menu. Please note that we are currently inserting this code snippet in somewhat of a *"dangerous"* manner, by having the entire snippet pasted into a textarea that is then inserted into wordpress. Please take care when making any modifications to this, and be sure to test all changes in preprod first. It was built this way due to tight deadlines and multiple code snippet revisions from the Salesforce team, however going forward we should refactor it so that it has a safer implementation.

**In order to get NU-ton to live within our existing "menu button popup", the following addition to the Salesforce-provided code snippet is critical:**

    const targetEl = document.getElementById('chatbox_container');
    embedded_svc.settings.targetElement = targetEl;

This should occur directly before the `embedded_svc.init()` function is called.

## Troubleshooting

**If we need to turn off everything**, go to wp-admin: Chatbox menu, unclick 'enable sitewide chatbox'. This will turn the entire chat functionailty off site-wise (i.e. the floating chat icon will disappear altogether).

**If we need to turn off only livechat**, go to wp-admin: Customizer -> Web Services Integraiton -> Livechat, and toggle off.

**If we need to turn off only NU-ton**, go to wp-admin: Chatbox menu, and delete the 'code snippet'. *Please save a copy of the code snippet locally before doing this as there is no way to recover it from within wordpress*.


Helpful contacts:
Michael Hicks (MST Team) - Software Engineer overseeing NU-ton development

TESTING TESTING 10/8/2025

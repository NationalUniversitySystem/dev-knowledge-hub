# Trustpilot Integration

All remaining trustpilot code is legacy code that can be removed. There were multiple Trustpilot initiatives we implemented in the past. All of them were deemed high-priority at the time, but later turned out to be complete wastes of time due to poor leadership decisions.

## Embedded Reviews Widgets
On certain pages we display reviews from Trustpilot (or at least we did at one point).

## Email API
Our email marketing team will occasionally send out emails to students prompting them to leave a review on trustpilot. In order to make this review process as frictionless as possible (i.e. can submit a review without signing in or creating an account), we need to pass certain encrypted data to Trustpilot. We accomplish this via a custom-built API on our site.

The code for this lives in a custom plugin: plugins/nuedu-trustpilot. While on it's own this wouldn't be enough to warrant it's own standalone plugin, going forward we should try to migrate the above-mentioned embedded reviews functionality into this plugin as well.
# About Google Analytics

Google Analytics is a tool for gathering information on what page(s) of a site are visited and how often, where web visitors traverse fromt-and-to within a web site, and whether visitors ultimately become "customers".

The following is a collection of notes about Google Analytics, and more generally web analytics. The purpose is to reinforce key concepts for learning the topic, and implementing analytics in future web sites.

## Table of Contents

- [Introduction](#introduction)
- [Google Analytics 4](#google-analytics-4)
- [How GA4 Works](#how-ga4-works)
- [Differences Between GA4 and Universal Analytics](#differences-between-ga4-and-universal-analytics)
- [Some GA4 Features And Reports Overview](#some-ga4-features-and-reports-overview)
- [GA4 Types of Reports](#ga4-types-of-reports)
- [Google Marketing Platform Account](#google-marketing-platform-account)
- [GA4 Properties](#ga4-properties)
- [GA4 Data Streams](#ga4-data-streams)
- [GA4 Google Tags](#ga4-google-tags)
- [References](#references)
- [Footer](#footer)

## Introduction

Values of Analytics:

- Acquisition: Build awareness and interest in the organization and business.
- Behavior: What do web visitors do while on interacting with the site, and where do they navigate to?
- Conversion: A visitor becomes a registered user and/or enters some transaction with the business.
- Work with Google Ads to draw interest to the web site.

More Insights:

- Which marketing efforts are working well? Focus on those and abandon others.
- Where do web users have difficulties on the web site? Change the site navigation (or page layout or content) to help users successfully reach their goal.
- Align on-site advertising with interests of visitors.
- Understand customer online purchasing habits to inform future marketing.
- Lead Generation: Sales can connect with potential customers with these references from analytics.

Other Data Acquisition Sources:

- Mobile Apps.
- Online Point-of-Sale systems.
- Video-game consoles.
- CRM systems.
- Other internet-connected platforms.

Reports:

- Perform in-depth analysis.
- Better understand customers.
- Review results of new solutions to increase conversions, sales.

## Google Analytics 4

Aka GA4. Deprecates Universal Analytics (since July 2023). Is an application property that enables:

- Collection of web site and application data.
- Event-based (rather than session-based) data collection.
- Privacy controls: Cookieless, key event modeling.
- Predictive capabilities using simple models.
- Media platform integration.

GA4 can be implemented in the following scenarios:

- New web site or application.
- Existing web site or application using Universal Analytics (Analytics "classic").
- Using a CRM hosted web application: Wix, WordPress, Drupal, Squarespace, GoDaddy, WooCommerce, SHopify, Magento, Awesome Motive, HubSpot, etc.

Note: Firebase applications _are supported_ in GA4.

## How GA4 Works

1. Data is collected from within the application or web site using JS code.
2. A database stores the data.
3. GA4 reporting site displays results of GA4 data collected by the scripts.

What is collected?

- "Pseudonymous information" about the user.
- Counts of users that visited a page, area, or successfully completed a purchase confirmation page.
- Visiting user Browser information including language and version.
- Whether the user device is a mobile phone, tablet, PC, etc.
- Where the user "came from" if navigated from another web site or domain such as an online Ad, or an email marketing campaign.

Collecting and Reporting

- JS code packages and sends data to GA4 database.
- Data is aggregated and organized for review on reporting pages.
- Configuration allows customizing what data to collect and report on.
- Database Data _cannot be changed_.

## Differences Between GA4 and Universal Analytics

- Data Model: GA4 is event-based, UA is event-based. In GA4, every click and other interaction with a page results in reportable data points.
- Device-type and platform statistics are properties of reported data in GA4. In UA, device-type and platform properties are reported separately. Google calls GA4 measurements 'enhanced' and 'more comprehensive' than UA.
- GA4 includes engagement and monetization reports, including traffic and acquisition reports.
- IP address privacy and data deletion are available in GA4, as well as the ability to turn-off location-specific data.
- Website and App performance characteristics are reportable in GA4.
- Engagement per session in GA4 biases toward engagement instead of 'bounce' like UA does.
- UA and GA4 count conversions differently, and multi-click events in same-session are accumulated in GA4, but not in UA.

## Some GA4 Features And Reports Overview

- Accounts and Properties depend on what you have access to, and how many website GA4 is configured for.
- Have a separate account for each business or web site you administer.
- "Property": A set of reports for a web site.

> Think of a GA4 Account as a folder that hold the statistical data that is collected.

## GA4 Types of Reports

Available from the Google Marketing Platform site.

- Reports Home: Top-level overview of metrics such as users, conversions or important actions, events (page views, link clicks, video watches, etc), total sessions. Tracks current 28 days and preceding period simultaneously. Also categorizes visitors by country.
- Reports: Snapshots of acquisition, engagement, monetization, and retention statistics. Drill-down into more details for each category.
- Explorations: Create other report types.
- Advertising: View dedicated "attribution reports". Relationships between marketing channels and user conversions.

## Google Marketing Platform Account

- Think of your Google Anaytics account as a folder that stored GA4 data.
- Additional accounts can be created. Suggest 1:1 with business to GA4 Account.
- Properties: Used to report on an individual web site (although multiple web sites and apps can be collected into a single Property). Name the Property appropriately for the web site (or selection of sites/business) it is for.

## GA4 Properties

When creating a Property, it is good to stick with a 1:1 relationship with a single web site, or "business" such as a collection of sites and apps.

- Add a category and size of business to the Property.
- Select business objectives. This configures reports for you. Selecting "Baseline Reports" is a good idea as it allows the most capability.
- Create a Data Stream for a single web site, or multiple Data Streams (one for each platform).

## GA4 Data Streams

Types: Web, Android, or iOS.

- Needs an endpoint/url and a name.
- Enhanced meaasurement: Enabled by default but can be disabled wholly, or some of the actions it tracks.

## GA4 Google Tags

Overview:

- If existing Tags are found, the Data Stream can use it.
- Otherwise, use the Google Tag script code provided to install manually, or CMS/website builder.
- Measurement ID and Stream ID are used to ensure data flows from the target site(s) to the capturing Property.
- Other Tags (besides Google Analytics) can be used, and managing those is allowed within the admin utility.
- Tag Manager requires an account, separate from the GA4/Marketing Platform account. Use a name that helps identify which web site or app the Tag Manager is set up for.
- Tag Manager creates a Container, and generates Container Code (JavaScript) that must be added to every page of the site (some in the header, one - the No Script code - in the body).

Wordpress:

- Has a Plug-in to allow configuring Google Tags.
- Need the Container ID in order to set up the Plug-in.
- Wordpress propagates the code block automatically using the Plug-in.

Configure a Tag:

1. New Tag.
2. Name according to the type of report data you want to capture.
3. Select a Tag Configuration, such as "Google Tag". These might require a "Measurement ID".
4. Configure a Variable so that the Measurement ID can be used in multiple Tag configurations.
5. Save the Tag.
6. Publish the changes.
7. Wait 24hrs to see data in reports.

_Note_: There are several variable 'types', and an appropriate one should be selected.

_Also Note_: If your site has multiple Tags, there might be additional configuration necessary before publishing a newly created Tag.

## Setting up GA4

Since UA stopped collecting data in July 2023, GA4 is the currently supported (and active) analytics model service.

Overview of steps:

1. Setup a Google Analytics and Tag Manager accounts.
2. Create a Property in the account and copy the Measurement ID.
3. Login to Tag Manager and create a new Configuration.
4. Select GA4 Configuration and enture the Measurement ID acquired previously.
5. Select 'Send a Page View Event' option.
6. Click 'Triggering' and select 'All Pages'.
7. Submit and Publish.

Detailed [Set up analytics for a website and/or app](https://support.google.com/analytics/answer/9304153?hl=en) instructions.

Reminders:

- Enhanced Measurements are enabled by default. These can be disabled.
- Cross-domain tracking must be configured when two domains should be tracked with the same Property.
- Individual IP addresses must be added to define 'inernal traffic'.
- Google Ads can be configured separately.
- Conversions must be configured for the Events you want to track conversions with.

## References

- [Google Analytics 4 Tutorial 2024 - How To Get Started With GA4, by Loves Data](https://www.youtube.com/watch?v=OIVhhgNQjak)
- [Set up analytics for a website and/or app](https://support.google.com/analytics/answer/9304153?hl=en)

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).

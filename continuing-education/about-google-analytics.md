# About Google Analytics

Google Analytics is a tool for gathering information on what page(s) of a site are visited and how often, where web visitors traverse fromt-and-to within a web site, and whether visitors ultimately become "customers".

The following is a collection of notes about Google Analytics, and more generally web analytics. The purpose is to reinforce key concepts for learning the topic, and implementing analytics in future web sites.

## Table of Contents

- [Introduction](#introduction)
- [Google Analytics 4](#google-analytics-4)
- [How It Works](#how-it-works)
- [Differences Between GA4 and Universal Analytics](#differences-between-ga4-and-universal-analytics)

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

## How It Works

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

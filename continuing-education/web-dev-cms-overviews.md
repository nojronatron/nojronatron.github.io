# Web Site CMS Overview Notes

Content Management Services allow customers to create, edit, deploy, manage, and promote their web sites, whether they are commercial, governmental or NGO, or personal.

This page is a selection of notes taken while looking into various available CMSs.

## Table of Contents

- [SquareSpace](#squarespace)
- [SQSP Forms](#sqsp-forms)
- [SQSP Member Sites](#sqsp-member-sites)
- [SQSP Customer Accounts](#sqsp-customer-accounts)
- [SQSP Paywall Areas Website](#sqsp-paywall-areas-website)
- [Resources](#resources)
- [Footer](#footer)

## SquareSpace

Accepted abbreviation: SQSP.

### SQSP Getting Started

Creating a new site:

- Pick a specific template for the first page.
- SS will ask questions to select a template for you, however it might not be what you want.
- Templates are just a starting place.
- Template pre-define Style, Layout, Fonts, and Colors, but these can be customized.

Questions:

> Is it possible to build a site without a template?

Yes, but more correctly put, build a _page_ for a site starting as a blank page, or using a template.

### SS Design Tools

Views:

- Desktop and mobile viewing switcher.
- Build in one view, update in both views to tweak UX.

Search:

- Search tools within other tools exist to find a specific one.
- Use the `/` key to bring-up the search tool at any time.

Fonts:

- There are millions to choose from.
- Ligatures, weight, etc can be customized during design time.
- Font Packs: Contain pairs of "complimentary" fonts.
- Font overlap between SS and Canva, simplifying Canva-to-SS design and deployment.

Template Color Palettes:

- Presets: Contain some reasonable palettes with 6 (or so) shades of "complimentary" colors.
- From Image: Will choose a palette of colors based on an uploaded image.
- Custom Picker: Select your own colors and shades and assign to the palette.
- Other Colors: Modify an existing color and set as a palette color for this site.

> Do Color Presets utilize Accessible Design Practices?

Add Page:

- Tied-in to main Navigation.
- Provides templates to choose from.
- Some templates are basic pages, others are more specific (Blog posts, etc), so look through the entire list.

Navigation:

- Nav Bar is automatic and displayed on the page(s) by default.
- Nav Bar drop-downs are allowed, requiring a few extra clicks.
- Home Page can be removed from the navigation tree.

> Are there other navigation linking options besides a header-based Nav Bar?

- Use Anchor links to other areas internal (or external) to the site.
- Use buttons with anchor links (although this is discouraged for accessibility reasons).

Asset Library:

- Photos and other assets can be stored here.
- Before uploading images, rename using A11y and SEO best practices.

Page Blocks:

- Contains controls like Buttons, Textbox, etc.
- Select, configure, place WYSIWYG style.
- Buttons can be used to link to URLs including local (using Navigation), or remote (using Anchor elements).

Sections:

- Add, remove, or shift sections on-screen, WYSIWYG.
- Sections can be added using a Template or a blank section element.
- Modification of Section location is possible to widen or shrink Section sizing.
- Section sizing will affect content placement and size restrictions.
- Click the :heart: icon to 'Save Section' and it will appear in the Website Edit Nav Bar under 'Add a Section' :arrow_right: 'Saved Sections'. Just be sure to update the Form Name and its connection (storage, email, etc).

Higher Level Features:

- Selling: It is possible to add-on a shopping-cart style section of the site. Fees apply.
- Marketing: Campaigns and newlsetters can be configured, scheduled, and monitored. Fees might apply depending on volume.
- SEO and Analytics: Google Analytics are used to capture visitor behavior, conversion rates, etc.
- Contact: TBD.
- Scheduling Templates: TBD.
- Plug-ins: SS makes some plug-ins available, and allows other plug-in usage.

_Note_: Newsletters and downloads can be configured in the Marketing Tool. Fees may apply depending on volume.

_Note_: SquareSpace plug-in config and usage might be easier than other CMS vendors (anecdotal comment).

## SQSP Forms

- Can be styled with up to 4 built-in styles, or any of those styles can be customized within the Forms properties modal.
- Field Options: Shape, Fill, Thickness, Size, Spacing, Color, and Layout.

Custom Form Styles are made available across the entire _site_.

Form Email Field(s):

- There is a Sign-up field that can be enabled on the form.
- Can be made to be _required_.
- Email sign-up can send a _confirmation email_.

Form Data Storage:

- Submissions: Provides a view into 'Form Submitters' and other lists of interactions and the web visitors such as 'Subscribers', 'Customers', 'Leads', 'Donors', etc.
- Email Notification: Configure _one_ email address to notify when Form Data has been captured.
- Set 'Additional Storage': Choose from Google Drive, Zapier, or MailChimp.
- Enable Google 'reCAPTCHA':

Look at 'Smart List' called 'Form Submitters' to view a list of website users that have submitted a Form.

- Click-in to the user entry to see the information they submitted via the Form.
- Create a 'Project' (there's a link within the Form Submitters user properties) to manage Invoices, client information, and other details.

Data Storage and Selling (tm):

Known as 'clients', these represent website users that may receive an 'Invoice', so their data is captured and maintained.

1. Open the 'Selling' config nav item.
2. Open 'Invoicing'.
3. Create 'New Client' or view existing 'Clients'.
4. Click 'Invoicing' and search the list to select the Client to Invoice.
5. This opens a New Invoice (or lists existing ones). New Invoices can have line items added to them, a due date can be set, and a Memo can be added (such as 'Thanks for your order!').
6. Once created, the Invoice can be sent to the Client using the 'Send' button (confusingly, located in the upper right-hand corner of the 'Invoice Draft' screen).

## SQSP Member Sites

Automatically Paywalled.

1. Update pages of Member Site with the page types/layouts/styles you want.
1. Select single, or multiple prices.
1. Select Free, Subscription, or single-purchase order with cost.
1. Add a "Digital Product Block" to a public page to allow visitors to sign-up for membership, and create an account to access the content.

About:

- A Digital Product Block should be used to create a _public accessible LOGIN PAGE_.
- The first page in Member Site is the site's homepage.
- Drag-n-drop other page to the top position to change the Member Site homepage.
- Pages that are already part of a pricing plan _cannot be drag-n-dropped into a Member Site_, instead _duplicate the page_ and then move the duplicate.

Advice: Keep Member Site page count low so the list of pages does not cause a poor UX for the user.

SEO: This is _disabled_ in Member Sites by default (so is password protection).

## SQSP Customer Accounts

- Web visitors can store payment methods, shipping addresses, and past orders.
- Customers can create account during the checkout process.
- Customers can use Login link to sign-up.

To Enable:

1. Go to Administration page.
1. Open Commerce area.
1. Look for 'Customer Accounts' and set to: ON

You Can:

- Customers with accounts are indicated in the Customers list.
- Order history and contact information is available.

## SQSP Paywall Areas Website

## Resources

- [Complete Squarespace Tutorial 2024 (For Absolute Beginners) by Paige Brunton](https://www.youtube.com/watch?v=VcmfNO_Vpe8).

- [Squarespace Pricing: Know Before You Buy, by Steve Builds Websites](https://www.youtube.com/watch?v=3i_ScvYXlOs).

- [Squarespace Review 2024 - The Good, The Bad And The Ugly, by ImminentWebsite](https://www.youtube.com/watch?v=cZDBcOY57Ek).

## Footer

Return to [ContEd Index](./conted-index.html).

Return to [Root README](../README.html).

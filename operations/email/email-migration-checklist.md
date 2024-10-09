# Passion Dental Email Migration Checklist

This guide is for IT staff at Passion Dental. It is for internal use only.

## Overview

The guide will cover the following topics:

* Migrating the Domain to Amazon Web Services (AWS) - not done
* Migrating name servers (i.e. DNS services) to Cloudflare - not done
* Setting up the domain on Office 365
* Setting up MX records
* Setting up SPF records
* Setting up DKIM keys
* Mailbox imports - not done

### Adding domain to Office 365

Domains are automatically added to Office 365 when the location has a primary domain checked on the `Passion Dental Domains` smartsheet. You can find that sheet <a href="https://app.smartsheet.com/sheets/gw6ggxhMfhg32qpFc22vQh84w6rV2xHC37Q7H5w1?view=grid" target="_blank">here</a>. 

Note: that sheet flows to the Passion Email Domains sheet under the "Desired Domain" column. You can find that sheet <a target="_blank" href="https://app.smartsheet.com/sheets/3rX4ffcF5F7M625fpghq4m76Fhp5hJ8qX86379Q1?view=grid">here</a>.

In order to add a domain, complete these steps:

* Add the domain to the Passion Dental Domains for the given location
* Check the box "Primary Domain" and "Email"
* Wait 24 hours for the Sensu Check to automatically add the domain.

The Sensu check that adds the domains automatically can be found here (must be on the Passion network): https://sensu.passiondental.ca/n/production/events/PGFS01/smartsheet-setup-o365-domains

### Setting up MX records

Since we add our domains automatically, you can visit the Domain settings page to see a list of domains we have.

In order to add MX records for a particular domain, follow these steps:

* Go to the domain setting page here: https://admin.microsoft.com/#/Domains
* Click on the domain you're adding MX records for
* Click on "Setup"
* You may need to verify the domain.
  * We use Cloudflare as our DNS provider, so you will need to login to Cloudflare to validate Passion's ownership of the domain.
* Once the verification is complete, check the box for "Exchange and Exchange Online Protection"
* Click "Add DNS Records" to add the required DNS entries to Cloudflare automatically.
  * *NOTE:* Microsoft tends to use the softfail SPF flag `~` and we prefer the hard fail flag of `-`, so please go edit this after the DNS records have been added. See the SPF record section below for more information.

We have monitoring to ensure our domains have the correct MX records set for each domain. You can find the check here: https://sensu.passiondental.ca/n/production/events?filters=check%3Adomain-check-mx&limit=200&offset=0


### Setting up DKIM keys in Office 365

Durign the setup of the MX records, Microsoft Office 365 may have already configured DKIM. In the event it is not configured, please continue reading. 
In order to get DKIM signing setup with Office 365, you need to add some DNS entries. Follow these steps:

* Visit the email authentication page in the security admin centre.
  * Link: https://security.microsoft.com/authentication?viewid=DKIM
* Click on the domain you want to setup DNS entries for
* Under the "Publish CNAMEs" section, copy the selector for each domain.
  * The format is usually `selector1._domainkey.<domain_name>.com` and `selector2._domainkey.<domain_name>.com`
* Once these CNAME entries are added, hit the toggle at the top for "Sign messages for this domain with DKIM signatures".

We have a Sensu check to ensure we have a `selector2` on each domain running. You can view the results here: 
https://sensu.passiondental.ca/n/production/events?filters=check%3Adomain-check-dkim

### Setting up SPF records for Office 365

During the setup of the MX records, Microsoft Office 365 may set the SPF already. Microsoft usually uses the softfail flag and may not have included some of our other services. 
We have a Sensu check running to check if our SPF records are configured correctly. You can find the results of that check here: https://sensu.passiondental.ca/n/production/events?filters=check%3Adomain-check-spf&limit=200&offset=0

As of October 9, 2024, our standard SPF record is

````
v=spf1 a:dispatch-us.ppe-hosted.com include:spf.protection.outlook.com include:mail.zendesk.com include:_spf.intacct.com -all
````

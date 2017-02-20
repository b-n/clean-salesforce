# Clean Salesforce
A development guide for Salesforce (functional and technical)

## Table of Contents

  1. [Introduction](#introduction)
  2. [Development Principles](#environment-and-sandboxes)
  3. [Objects and Fields](#objects-and-fields)
  4. [Profiles and Permissions](#profiles-and-permissions)
  5. [Role heirarchy](#role-heirarchy)
  6. [Workflow automation](#workflow-automation)
  7. [Record Types](#record-types)
  8. [Deployment methods](#deployment-methods)
  9. [Apex classes](#apex-classes)
  10. [Triggers](#triggers)
  11. [Lightning](#lightning)
  12. [Visualforce](#visualforce)

## **Introduction**

This is a shameless pull from [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)

The idea is to generate a single style guide for developing on salesforce, both
functional (point and click), and the technical (code, apex, lightning) realms.
All to often do we find a project which has had many different people touch it
over a period of days/weeks/months/years, all with different styles.

As per clean-code-javascript, not all principles below are designed to be followed
strictly and to the point. This is just to serve as a general guide and possibly
as a way to pick a direction so you can fail fast and fail quickly - rather than
spending hours debating on the correct principle to use.

Everything starts with mistakes, drafts can be error prone, but with some luck
this guide will help point you in the right direction from the start

## **Environments and Sandboxes**
### Build everything in sandboxes

**Bad:**
- Developing in production
- Having different permissions in prod vs. dev
- Having fields that exist only in prod
- Changing a page layout only in production

**Good:**
- Profile changes are made in a sandbox
- All profiles are added to changes sets
- Standard reports and built in a sandbox
- You deploy a page layout - and it doesn't break anything

### Never develop directly into production
It's 2017 and I feel as though I still need to say this.

**Bad:**
- Developing prod

**Good:**
- Not ruining your environments

### If you're forced to develop into Production, replicate to dev sandbox
Ok, the off chance you need to change a page layout in prod, or some other well
crafted excuse, make sure you replicate these changes down.

It's worth noting that this might not have ever affected you, but it surely has
affected someone else. A technical developer can get a requirement to do something
with a field which is relied on by users in production. More often than not, the
technical developer will just create this in dev - probably getting the data length
(text), permissions, or even API name wrong. This adds additional effort to the
development lifecycle which could be easily avoided by replicating the changes down

**Bad:**
- Leaving your changes in production and the changes being overwritten in the next deployment

**Good:**
- Making the change in your main development sandbox as soon as you made the change

You may not think it's worth it today, but this will save your bacon later

### Ensure profiles/roles are set up correctly in the sandbox
See the [Profiles and Permissions](#profiles-and-permissions) section, as well as the [Role Heirarchy](#role-heirarchy) sections for
more information on how to set these up, however these should be developed in
the sandbox from day 0.

**Bad:**
- Only creating profiles in production
- Changing permissions in different sandboxes

**Good:**
- Profiles and Roles are scoped early
- Profiles are always added to all changesets

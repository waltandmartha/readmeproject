### THIS IS README ME

## OUR CLIENT

back2bikes is a social enterprise, providing bicycle training, repair and recycling services for the local community, asylum seekers and refugees.

back2bikes is run by volunteers, and is supported by Port Phillip Council.

They are looking for:

*  New volunteer mechanics (no skills required)
*  New volunteers to promote us
*  Donations of usable bikes and parts
*  Bike servicing

They offer:

* Quality secondhand bikes for sales
* Cheap servicing and parts
* (Paid) Maintenance courses
* Free training for volunteers
* Bikes for refugees and asylum seekers

We are happy to be involved with an organisation that helps the community and is not for profit.

## THE CLIENT'S PROBLEM

back2bikes buy all of their parts from one supplier, Bicycle Parts Wholesale and they do not provide RRP (Recommended Retail Price) to them.
At present they can't hide the trade price from the customer when looking at their web site. 

http://www.bicyclepartswholesale.com.au/page/10/product-catalogues

Bicycle Parts Wholesale (BPW) publish a glossy colour catalogue, which is essential when placing orders, as the photos on the web site and the descriptions are not always adequate to work out which part to order.

back2bikes have a CSV file of their database. It is simply a list of a part number, a short description and a bar code number. No category or sub-category information is available.

So we need to do the following:

* Import the parts list and prices to our (Mongo) database
* Provide a simple page (within our existing Meteor app) to allow searching of the database, either by name or part no
* Write an algorithm to calculate a RRP
* Display the price of the part(s) found as a list
* Provide an advanced search option

### Possible extension: 

* Allow part to be added to a draft order, with a quantity
* Review draft order, add/remove parts
* Send order to supplier (via email)
* BPW will send us updates the price list every now and then. An update process should allow an import of the new CSV file, but it should be checked to make sure that 1) The number of items should be +/- 10%, average prices should also be +/- 10%

All to be done using React, Storybook, TDD

## Pricing algorithm

* The first calculation is to double the wholesale price to make RRP. 
* This helps to cover GST and shipping costs.
* For more expensive items, we don't need to make so much, so for anything costing over $60, we mark it up by 50%
* Anything over $100 wholesale we mark it up by 30%



## SOURCE CONTROL PROCESS

Git branching strategy.

### master

The master branch corresponds to the code that is currently in production. Every time we do a deployment to production, we put a tag in git, so that we have a way to go back to a particular release (in case we ever need to). This branch is protected to prevent accidental updates

### develop

The develop branch corresponds to the code that is currently on the staging server. Similarly these versions are tagged in git when we deploy them, and the branch is also protected.

### feature/xxx branches

Feature branches are for developing particular features, for example a feature to add a part to an order might be named feature/order-add-part. 

All branches should be created from develop.  You should never create a branch from another , unless there is a dependency on code in that branch.

### fix/xxx branches

If you are making changes to address a bug that is not urgent, you should use a branch name like fix/xxx. This change will go through the regular release workflow just like feature changes.

### hotfix/xxx branches

If you are making changes to address a bug that is urgent, and needs to be installed without delay, then you can use the hotfix prefix. The branch should be created from the master branch, as it will be merge directly into master, and deployed from there. This workflow is unusual, and does not follow the regular release procedure. It should be limited to small changes, to minimise the risk of failure.




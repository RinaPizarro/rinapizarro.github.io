---
layout: post
title: Use Relationship
categories: powerbi
description: This guide will explain the usage of USERELATIONSHIP() and inactive
  relationships in PowerBI.
---
PowerBi allows for one active relationship at a time. If Table A has CustomerID and SalesID, but Table B has only SalesID, we can create an active relationship between Table A and Table B on SalesID. When we add the CostID from Table B to a visual, we can also add the CustomerID from TableA and PowerBI will be able to pull the CustomerID from Table A. Relationships as structured as

1. One Side (Lookup table)
2. Many Side (Fact table)

Having only one active relationship prevents confusion for PowerBI. If a lookup table had both CustomerID and ProductID as the key, PowerBi wouldn't know which to look at.

If you want to use an inactive relationship, you will need to tell PowerBI to use the inactive relationship with USERELATIONSHIP().
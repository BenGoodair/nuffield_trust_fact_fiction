# Social Care Market - Fact or Fiction?
 
Welcome to a holding repository for underlying data and explanations for a Nuffield Trust briefing on the adult care home market.

# What is available?

The repo currently holds data files and final figures used in this article [link].

The repo is structured with a master dataset of all care home and domiciliary care locations, and their characteristics stored in the "underlying data" folder. The underlying data includes for each care location: it's open and close date, type of provision, ownership category, provider name, area deprivation, and average overall inspection rating across the location's lifetime.

Then there are also csv files for the numbers underlying each figure in their own folders.

# How did we create the data

## CQC data

To download the data - we ran python code calling the CQC API for each location and provider, harmonising all inspections and locations ever registered to the CQC. An old version of this code is published [here](https://github.com/BenGoodair/adults_social_care_data/blob/main/Code/Location_rating_pull.py). If you want our up to date python code which pulls and harmonises full CQC API data, email me (see bottom), I'd be happy to share this.

We then classify all care homes by the CQC's binary flag carehome y/n. And we classify all domiciliary care locations as any location where the location's primary inspection category is "Community based adult social care services".

We convert all historic overall ratings (Inadequate, Req improvement, Good, Outstanding) into a four scale numeric variable (0,1,2,3). And average that for every location, based on the CQC's Location Id

Finally, we coalesce each location's provider name with the CQC "Brand name" column to identify operational chains in our provider column.

## Ownership classifications

We undertook a large process of ownership classification to identify a nuanced reflection of market providers, they are defined below.

 - Non profit: operating provider has a charity number.
 - Council: NHS or LA organisation which runs services (based on name searches).
 - Individual owned: Is run for-profit, but the owner reports no company number representing an individual or partnership ownership model.
 - Corporate owned: Is run by a for-profit company, has no charity number, has no investment owner.
 - Investment-owned: any home which was run by a company which as of 2026 has shareholding by an investment firm.
   * Where an investment firm is any company with a nace code of 64, 65, 66
   * Or a firm name includes any of the following terms: "topco", "seniorco", "newco", "midco", "bidco", "opco", "equity", "partner", “capital”, “venture", "althea investments", "welltower".
   * And where “shareholding” relates to any of the following: shareholders, persons of sig control, controlling shareholders, ultimate owners. And the shareholders, persons of sig control and ultimate owners of all of the immediate shareholders, persons of sig control and ultimate owners.

There are some considerations to understand in relation to this ownership classification. First and foremost, we access the data using FAME's Moody's interface. One of the difficulties of this is that the interface returns no shareholding for dissolved firms - therefore our estimates of investment ownership historically are going to under-represent true levels. Our classification also often misses out REITs - which do not have the same corporate structure as private equity firms and often do not have "midco" type firms in their corporate structure.

# Notes and considerations

Please reach out to b.goodair@lse.ac.uk for questions - I am very happy to share bespoke code/ data as per requests and individual needs.

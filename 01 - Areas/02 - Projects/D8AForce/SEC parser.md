AKA xml parser

**Steps**:
- loop over `.xml` files from the resources
- select all `Indvl` elements 
- duplication check (crd)
- process current employers (creates or reuses company; connector)
- creates the Investor entity
- saves everything to db

In general it uses the data from the same service like [[Adviser-info parser]], but it is offline, makes no requests, works only with xml files.
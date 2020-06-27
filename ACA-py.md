
## [Home](./README.md)

## ACA-py (Aries Cloud Agent - Python)

**Am I correct in assuming that ACA-py currently has no "discovery" capability in terms of searching the Ledger for matching Schemas or Credentials ? I note that you can fetch these by exact Id, and the Issuer Wallet can fetch all the ones that they have created. Is the intention that any Potential Holder must obtain an Id out of band to initiate the "Propose Credential" message in RFC0036 ?**

* It's not so much ACA-Py as Indy Node that does not support that. We are talking about ways to support that in indy-vdr in the future. For now, you can create your own or use a service like indyscan.io or https://sovrin-mainnet-browser.vonx.io/ to query the ledger. Each of those read all the transactions, put them in a database and allow you to search them in a browser or using an API. Once you have the transactions of interest, you should still check them on the ledger -- especially if you get them from a service you don't operate. Having said that, there is little to be gained from anyone putting up fake info...

## [Home](./README.md)

*For more details of the aries [concepts](https://github.com/hyperledger/aries-rfcs/tree/master/concepts) & [features](https://github.com/hyperledger/aries-rfcs/tree/master/concepts) beyond the scope of the FAQs, please refer the [Aries RFCs](https://github.com/hyperledger/aries-rfcs) repo*


## Aries & ACA-Py (Aries Cloud Agent - Python)

### ACA-Py

**Am I correct in assuming that ACA-Py currently has no "discovery" capability in terms of searching the Ledger for matching Schemas or Credentials ? I note that you can fetch these by exact Id, and the Issuer Wallet can fetch all the ones that they have created. Is the intention that any Potential Holder must obtain an Id out of band to initiate the "Propose Credential" message in RFC0036 ?**

* It's not so much ACA-Py as Indy Node that does not support that. We are talking about ways to support that in indy-vdr in the future. For now, you can create your own or use a service like indyscan.io or https://sovrin-mainnet-browser.vonx.io/ to query the ledger. Each of those read all the transactions, put them in a database and allow you to search them in a browser or using an API. Once you have the transactions of interest, you should still check them on the ledger -- especially if you get them from a service you don't operate. Having said that, there is little to be gained from anyone putting up fake info...

**The "action-menu" concept in ACA-Py, I am trying to get my head around how that would be used ? Is there an example anywhere that might explain its purpose ?**

* The idea of it is that it works like an interactive voice response (IVR) system. Your mobile wallet app connects with a service. The service sends you an Action Menu of the services offered. The mobile wallet displays the list and you pick the one you want. That goes back to the service, which kicks off the process associated with that action. At the end of the process, repeat.
* [IIWBook demo](https://hackmd.io/jrWg2kw7QuWx9XS0R3_XPQ?view)

**Can the same ACA-Py agent be used for storing multiple identities?**
<a id="multi-tenancy"></a>
* Multi-tenancy (ability to store/use/manage separate wallets from different/same entity at the agent) is very limited at the moment (version 0.5.2). For example there's a global default endpoint which new connections will use (for creating invitation for eg) if a custom one isn't specified, and DIDs don't yet have their own configured. 

**[Can we store different wallets in the same ACA-Py agent instance?](#multi-tenancy)**
Design a stock broker

Specifically what are we talking about? Are we referring to a stock exchange or are we referring to a market maker or are we referring to the likes of Fidelity and TDAmeritrade?
Fidelity and TDAmeritrade

What functionalites do we require? Can users trade options, make short sales, limit orders, GTC orders, etc.?
Just buy and sell of US stocks

Assume high availability as each second can mean millions of money lost

How many trades do we expect to be placed on a given day?
1million

When a user logs into their trading account, the user can place a trade. To place a trade, the user has to fill out a form in the UI that specifies: ticker, qty, px, side (buy or sell), orderType (mkt or limit order). There are cases where the ticker name could be duplicate, where a a ticker name can represent different companies' stocks trading in different exchanges; so the user cannot just type the symbol; as the user types the symbol in the dropdown, there will be a debounced api call that will query database of all trading symbols like the symbol the user has typed; the user must choose one of those once the user chooses that trading symbol, the UI will hold the state of the symbol metadata, that will probably specify the SymbolID as well as the exchange.

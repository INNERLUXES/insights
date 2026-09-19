# What we check before a smart contract goes to mainnet

Canonical version: https://innerluxes.dev/blockchain/smart-contracts-development

A deployed contract is hard to change and often holds value, so most of the work is in what happens before deployment.
No process can promise a contract free of every flaw, and we do not. What we do is make each of the checks below a
step you can see.

## Does this need a smart contract at all

Some problems are better solved with a database and an ordinary service. A contract earns its place where several
parties who do not fully trust each other need the same rules enforced and the same record to look at. If that is not
your case, we say so before you spend anything.

## Upgradeability and who holds the keys

We use proxy patterns where a contract has to change after launch, and we design who is allowed to trigger an upgrade:
a multi-signature wallet, a time delay, or both. An upgrade key held by one person is a weakness, so we agree the
admin model with you in the design phase and write it down.

## Testing beyond the happy path

Unit tests cover the expected flows. We add tests for the flows that go wrong: a caller who is not allowed, a repeated
call, a value at the edge of its range, an external contract that behaves badly. Where the logic handles funds, we
test it against a fork of the real network, not just a local simulation.

## Independent audit

Our own review is not a substitute for an independent audit when a contract holds meaningful value. We prepare the
code, the tests and the documentation for an outside auditor, and we fix what they find. Which auditor to use is your
decision, and we tell you what we would ask of them.

## Oracles and off-chain data

A contract that acts on outside data is only as reliable as that data. We decide with you where the data comes from,
what happens if it is late or wrong, and who can override it, and we build those cases into the contract rather than
leaving them to chance.

## Gas cost and deployment

We measure gas use per function during development, not at the end, and we rehearse the deployment on a test network
with the same scripts we will use on mainnet, so launch day contains no first attempts.

---

Related on innerluxes.dev: [Smart contract development services](https://innerluxes.dev/blockchain/smart-contracts-development), [Blockchain security](https://innerluxes.dev/blockchain/security).

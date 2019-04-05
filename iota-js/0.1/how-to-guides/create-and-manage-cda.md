# Create and manage conditional deposit addresses

**To send and receive transactions in an account, you must use conditional deposit addresses (CDA), which are special addresses that allow you to specify the conditions in which they are active and may be used for withdrawls and deposits.**

Accounts use CDAs to avoid address reuse. Without CDAs, recipients have no way of knowing whether a sender is about to debit an address before they credit it. With CDAs, recipients can create an address that expires after a certain time, allowing senders to make a judgement about whether to make a deposit. If senders aren't sure if a bundle will confirm in time, they can ask the recipient for another CDA.

:::info:
CDAs can be used only in an account and not in the generic [client library methods](root://client-libraries/0.1/introduction/overview.md). As a result, both you and the sender must have an account to be able to use CDAs.
:::

CDAs can be in either an active or expired state. Active addresses are part of the seed state, so they may not be used in withdrawals, but may be sent deposits. Expired addresses are removed from the seed state, so they may be used in withdrawals, but may not be sent deposits.

The workflow of a CDA should be the following:

1. You create a CDA
2. You send the CDA to a depositor
3. Based on the address's state, the depositor must decide whether a bundle will be confirmed in the given timeframe. If depositors decide the timeframe is too small, they should request a new CDA.

## Create a CDA

To create a CDA you specify the following conditions, which are used to determine if it's active or expired:

* **address (required):** An address
* **timeoutAt (required):** The time at which the address expires
* **multiUse (recommended):** A boolean that specifies if the address may be sent more than one deposit
* **expectedAmount (recommended):** The amount of IOTA tokens that the address is expected to contain. When this amount is reached, the address is considered expired. We highly recommend using this condition.

The combination of fields that you use to create a CDA determines if it can be used in withdrawals.

|  **Combination of fields** | **Withdrawal conditions**
| :----------| :----------|
|`timeoutAt` |The CDA can used in withdrawals as long as it contains IOTA tokens|
|`timeoutAt` and `multiUse` |The CDA can be used in withdrawals as soon as it expires, regardless of how many deposits were made to it. |
|`timeoutAt` and `expectedAmount`| The CDA can be used in withdrawals as soon as it contain the expected amount|
|`timeoutAt`, `multiUse`, and `expectedAmount` (recommended) |The CDA can be used in withdrawals as soon as it contains the expected amount (or more) of IOTA tokens |

:::warning:Warning
If a CDA was created with only the `timeoutAt` field, it can be used in withdrawals as soon as it has a non-zero balance even if it hasn't expired.

To avoid address reuse, we recommend creating CDAs with the `multiUse` field, even if only one deposit is expected to arrive at an address.
:::

---

Pass the CDA fields to the `generateCDA()` method

```js
const account = createAccount({
    provider: 'http://localhost:14265',
});

account.generateCDA({
    // Date in seconds
    timeoutAt: new Date('7-16-2186').getTime() / 1000,
    multiUse: true,
    expectedAmount: 10000000,
    security: 2
});
```

## Distribute a CDA

Because CDAs are descriptive objects, you can serialize them into any format and distribute them. For example, you can create a magnet-link for a CDA, with the `timeout_at`, `multi_use`, and `expected_amount` parameters.

```json
iota://MBREWACWIPRFJRDYYHAAME…AMOIDZCYKW/?timeout_at=1548337187&multi_use=true&expected_amount=0
```

:::info:
The `generateCDA()` method returns a serialized CDA as a magent link in a `magnetLink` field
:::

To parse a magnet link into a CDA, use the `parseCDAMagnet()` method

```js
const { address, timeoutAt, expectedAmount } = account.parseCDAMagnet(
    'iota://AT9GOVPQD...ADFA9IRSV?timeout_at=6833278800&multi_use=1&expected_amount:100000000'
);
```

## Deposit IOTA tokens into a CDA

After making sure that the CDA is still active, you can use the `sendToCDA()` method to deposit IOTA tokens into it

```js
account.sendToCDA({
    address: 'AT9GOVPQDDKAJ...ADFA9IRSV' // must include the checksum
    timeoutAt: new Date('7-16-2186').getTime() / 1000,
    expectedAmount: 10000000
});
```

You can also use a magnet link with the `sendToCDA()` method

```js
account.sendToCDA({
    magnetLink: magnetLink
});
```
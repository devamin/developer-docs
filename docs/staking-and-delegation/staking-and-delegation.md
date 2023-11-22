---
title: "Staking and Delegation"
---

# Staking and Delegation

## Delegation

TAO holders can delegate any amount of their stake to a subnet validator through a process called **delegation**. Delegation on Bittensor network works like this:

- A TAO holder, i.e., a delegator, also called a **nominator**, stakes with a subnet validator, making this subnet validator a **delegate** of the nominator.  
- The delegate (the subnet validator) then pools all such delegated stake, along with their own stake, and uses this total stake to perform validation tasks in one or more subnets. Daily staking rewards, in proportion to the total stake of the delegate, are credited to the delegate as a result of such validation tasks.
- After deducting a percentage for the delegate, these staking rewards are given back to the delegate's nominators. 
:::tip Delegate take %
The default value of the delegate take is 18%. As a delegate you can set your own delegate take % by using the `btcli root set_delegate_take` command. See [Setting your delegate take](#setting-your-delegate-take).
:::
- The above (100-18)% of the staking reward is distributed among the delegate's nominators in proportion to the nominators' staked TAO amount with this delegate.

:::info A nominator is a delegating authority
A nominator is the same as a delegating authority. Typically a nominator is an owner of TAO funds, looking to invest in Bittensor network without doing any validating tasks.
:::

## Delegate examples

### Becoming a delegate

If you are a registered subnet validator, you can become a delegate. To become a delegate:
1. You must make your hotkey available for the nominators. 
2. You must provide your delegate information and sign it.

The nominators will then delegate their TAO to this hotkey, i.e., the nominators will use your delegate hotkey as a wallet destination for their delegated TAO transfers.

#### Step 1: Nominate yourself as a delegate

Run the below command (for self nominating as a delegate):

```bash
btcli root nominate
    --wallet.name YOUR_WALLET_NAME
    --wallet.hotkey YOUR_HOTKEY_NAME
```

#### Step 2: Provide your delegate information 

Next, provide your delegate information, such as your delegate name, URL and description. This information will then be available in the list of active delegates, for example, when a nominator runs `btcli root list_delegates` to see available delegates. 

To provide this information and sign it, follow the instructions on this [Bittensor Delegates repo](https://github.com/opentensor/bittensor-delegates#2023-03-23---first-version).

### Setting your delegate take

As a delegate you can set your delegate percentage by running the below command:

```bash
btcli root set_delegate_take --wallet.name my_wallet --wallet.hotkey my_hotkey --take 0.1
```
where the value for the `--take` option is a floating point number between 0 and 1. In the above example, `--take 0.1` sets the delegate take as 10%.

## Nominator examples

### Viewing available delegates 

If you are looking for trusted delegate(s) to delegate your funds to, start by seeing a list of delegates who are already active on the Bittensor network. Run the below command on your terminal:  

```bash
btcli root list_delegates
```

You will get an output like this (click on the image to zoom):

[![List Delegates](/img/docs/list_delegates_screenshot.png 'Output of List Delegates')](/img/docs/list_delegates_screenshot.png)

See below for an explanation of the column headings in the above terminal output:

| Column | Meaning                                                 |
| :------ | ------------------------------------------------------------|
| INDEX   | Delegates with larger total stake are higher in the list. |
| DELEGATE | The name of the delegate. Click on the name to visit the delegate website. Only shows if the delegate has registered. |
| SS58    | The [SS58 hotkey of the delegate](../getting-started/wallets#list-all-the-local-wallets).                       |
| NOMINATORS    | The number of nominators, i.e., delegators, who have delegated to this delegate. This is also the number of unique cold keys (i.e., number of nominators) who have nominated **to** this hotkey (i.e., to this delegate).                       |
| DELEGATE STAKE(τ)    | The amount of delegate's own stake (not the TAO delegated from any nominators). This is the the amount of stake that the delegate-owned coldkey has delegated to this delegate's hotkey (distinct from TAO delegated from others).                       |
| TOTAL STAKE(τ)    | The total amount of stake delegated to this delegator's hotkey.                       |
| CHANGE/(4h)     | The percent change in the total stake delegated to this delegate within the past 4 hours.                       |                   |
| VPERMIT    | Shows the subnets for which the validator permits are held by the delegate. 
| TAKE    | Shows the delegate take percentage.                      |
| NOMINATOR/(24h)/kτ    | Stake reward distributed to this delegate's nominators within the past 24 hour period (per 1000 TAO). |
| DELEGATE/(24h)    | Stake reward cut taken by this delegate within the past 24 hour period.                        |
| Desc    | A description of the delegate.                     |

### Delegating tao

The below command will show a list of delegates sorted by their total stake. Select a delegate from this list to send your stake to.
```bash 
btcli root delegate
```

### Show your delegations 

To show all your previously made delegations:

:::tip
Use `--all` option to show delegations across all your wallets.
:::

```bash
btcli root my_delegates
```


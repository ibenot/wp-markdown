# General usage

The HiPay Wallet cash-out integration for Wordpress is intended to be used with a *cron*, but can be used directly from the command line. In fact, this software is supposed to execute tasks automatically, which is why you need to configure *cron* jobs (or any other alternative) that will execute commands at the appropriate time automatically.

Please note that default values for command line arguments/parameters are defined in the `parameters.yml`.

There are 3 main commands that need to be run automatically by relying on *cron* jobs:

- [Vendor processing](#vendor-processing)
- [Cash-out generation](#cash-out-generation)
- [Cash-out processing](#cash-out-processing)

There are also two debug commands that do not need to be run using a *cron* job:

- [Listing Wallet accounts](#listing-of-wallet-accounts)
- [Getting bank information](#getting-bank-information)

# Notifications

In some cases, the HiPay Wallet integration for Wordpress can encounter errors or issues that cannot be managed automatically. In such a case, a notification is sent by email in order to inform you about the issue. The email recipient can be configured in the `parameters.yml` file. When this documentation refers to a "notification" being sent upon error, it means an email notification.

# Available commands

## Vendor processing

### Command call

	$ php bin/console vendor:process

### Benjamin Code and Syntax Highlighting

```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```
 
```python
s = "Python syntax highlighting"
print s
```

```css
pre {
    font-size: 90%;
    line-height: 1.2em;
    font-family: "Courier 10 Pitch", Courier, monospace; 
    white-space: pre; 
    white-space: pre-wrap; 
    white-space: -moz-pre-wrap; 
    white-space: -o-pre-wrap; 

    height:1%;
    width: auto;
    display: block;
    clear: both;
    color: #555555;
    padding: 1em 1em;
    margin: auto 40px auto 40px;
    background: #f4f4f4;
    border: solid 1px #e1e1e1
} 
```
 
```makefile
BUILDDIR      = _build
EXTRAS       ?= $(BUILDDIR)/extras

.PHONY: main clean

main:
    @echo "Building main facility..."
    build_main $(BUILDDIR)

clean:
    rm -rf $(BUILDDIR)/*
```

```
No language indicated, so no syntax highlighting. 
But let's throw in a <b>tag</b>.
```

### Execution
1. Retrieves the vendors from Wordpress.
2. Saves the vendors: creates the HiPay Wallet account, if not already created, or gets the HiPay Wallet account number from HiPay.
3. Validates them.
4. Transfers the KYC files from Wordpress to the HiPay Wallet platform
5. Adds the bank information on the HiPay Wallet account if not already done or checks HiPay’s bank information against the data from Wordpress to make sure they match.
If these are not the same, an error notification is sent.

### Argument
|Name       |Type | Required | Description                           |
|-----------|-----|----------|---------------------------------------|
|lastUpdate |Date |No         |Date of the last update of Wordpress shops

### Options

|Name       |Type     | Description                           |
|-----------|---------|---------------------------------------|
|tmpPath    |String   | Path where the documents should be saved temporarily before being sent to HiPay Wallet

### Cron example
Please see below an example of how your cron job may be configured. Replace `path/to/bin/console` by the proper path to the `console` file.
This command should be run as often as the vendors update their data. 

	0 0 */7 * * php path/to/bin/console vendor:process `date +%Y-%m-%d`

## Cash-out generation

### Command call

	$ php bin/console cashout:generate

### Execution
1. Retrieves the *PAYMENT* transactions from Wordpress to get all the payment vouchers of the cycle.
2. Calculates the amount due to the vendors and the operator thanks to the retrieved payment vouchers.
3. Creates the operations to be executed afterwards, validates and saves them.

### Argument

|Name       |Type | Required | Description                           |
|-----------|-----|----------|---------------------------------------|
|cycleDate  |Date |No         |Sets the cycle date                    |

### Options

|Name               |Type       | Description                           |
|-----------        |---------  |---------------------------------------|
|executionDate      |String     |Date to consider for cycle date computing
|intervalBefore     |Interval   |Interval to subtract from cycleDate
|intervalAfter      |Interval   |Interval to add to cycleDate

### Cron example

Please see below an example of how your cron job may be configured. Replace `path/to/bin/console` by the proper path to the `console` file.
This command should be run right after the payment cycle has been made in Wordpress.

	30 0 1,11,21 * * php path/to/bin/console cashout:generate `date +%Y-%m-%d`

## Cash-out processing

### Command call

	$ php bin/console cashout:process

### Execution
1. Executes, on the HiPay Wallet platform, the transfer of operations in statuses *CREATED* and *TRANSFER_FAILED* dating from at least one day.
2. Executes, on the HiPay Wallet platform, the withdrawal of operations in statuses *TRANSFER_SUCCESS* and *WITHDRAW_FAILED* dating from at least one day.

### Arguments
This command doesn’t have any argument.

### Options
This command doesn’t have any option.

### Cron example

Please see below an example of how your *cron* job may be configured. Replace `path/to/bin/console` by the proper path to the `console` file.
This command should be run when you have payments you want to transfer to your sellers. Basically, after completion of the `cashout:generate` command.

	30 2 1,11,21 * * path/to/bin/console cashout:process `date +%Y-%m-%d`

## Listing of Wallet accounts

### Command call

	$ php bin/console vendor:wallet:list

### Execution
1. Retrieves the HiPay Wallet account information associated with a merchant group ID (associated with an entity)
2. Displays them in a table

### Argument

|Name       |Type | Required | Description                           |
|-----------|-----|----------|---------------------------------------|
|merchantGroupId  |Integer | No       |Merchant group ID for retrieving HiPay Wallet accounts                  |

### Options

This command doesn’t have any option.


## Getting bank information

### Execution
1. Retrieves the bank information status for a specific HiPay Wallet account ID
2. If that status is validated, displays the information stored by HiPay

### Argument
|Name       |Type | Required | Description                           |
|-----------|-----|----------|---------------------------------------|
|hipayId  |Integer | Yes      |HiPay Wallet account ID used to retrieve the bank information status              |

### Options
This command doesn’t have any option.

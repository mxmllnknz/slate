# Models

Here is the basic layout for all the data models used in this API.

## Account

Name                | Type              | Description
--------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------
id                  | unsigned int      | Unique positive integer identifier
is_partner          | boolean           | A boolean defining whether or not an account is a partner account (e.g. if a partner owns the account, not whether the account is linked to a partner site)
created_at          | date              | Date + time the account was created
updated_at          | date              | Date + time the account was lasted updated
deleted_at          | date              | Date + time the account was deleted (i.e. soft deletes)
transaction_history | Transaction[]     | See [Transactions](./#transaction)
balances            | Account_Balance[] | See [Account Balances](./#account-balance)

## Transaction

Name                   | Type         | Description
-----------------------|--------------|--------------------------------------------------------------------------------------------
id                     | unsigned int | Unique positive integer identifier
account_id             | unsigned int | Foreign key associated to the [account](./#account) of the primary party of the transaction
reference_account_id   | unsigned int | Foreign key associated to the [account](./#account) of the other party of the transaction
currency_id            | unsigned int | Foreign key associated to the [currency](./#currency) of the transaction
currency               | Currency     | See [Currency] (./#currency)
amount                 | float64      | The amount exchanged in the transaction
usd_cent_exchange_rate | int64        | The exchange rate between one currency and US Cents
kind                   | string       | The kind of transaction (e.g. send, receive, rewards)
description            | string       | A brief description of what the transaction was for
resulting_balance      | float64      | The balance after transaction of the account associated with the account_id
public_address         | string       | The wallet address of account_id if it was used in the transaction
created_at             | date         | Date + time the account was created
updated_at             | date         | Date + time the account was lasted updated
deleted_at             | date         | Date + time the account was deleted (i.e. soft deletes)

## Account Balance

Name        | Type         | Description
------------|--------------|---------------------------------------------------------------------------------
id          | unsigned int | Unique positive integer identifier
created_at  | date         | Date + time the account was created
updated_at  | date         | Date + time the account was lasted updated
deleted_at  | date         | Date + time the account was deleted (i.e. soft deletes)
currency_id | unsigned int | Foreign key associated to the [currency](./#currency) of the balance
account_id  | unsigned int | Foreign key associated to the [account](./#account) to which the balance belongs
amount      | float64      | The balance of [account](./#account) in this [currency](./#currency)

## Currency

Name          | Type         | Description
--------------|--------------|-----------------------------------------
id            | unsigned int | Unique positive integer identifier
currency_name | string       | Name of the currency in Flycoin database

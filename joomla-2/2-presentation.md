# PRESENTATION

## Cool joomla

| Field    | Type         | Null | Key | Default | Extra          |
|----------|--------------|------|-----|---------|----------------|
| id       | int(11)      | NO   | PRI | NULL    | auto_increment |
| miraklId | int(11)      | NO   | UNI | NULL    |                |
| email    | varchar(255) | NO   | UNI | NULL    |                |
| hipayId  | int(11)      | NO   | UNI | NULL    |                |

## Fun joomla

| Field          | Type         | Null | Key | Default | Extra          |
|----------------|--------------|------|-----|---------|----------------|
| id             | int(11)      | NO   | PRI | NULL    | auto_increment |
| miraklId       | int(11)      | YES  |     | NULL    |                |
| hipayId        | int(11)      | YES  |     | NULL    |                |
| amount         | double       | NO   |     | NULL    |                |
| cycleDate      | datetime     | NO   |     | NULL    |                |
| withdrawId     | varchar(255) | YES  | UNI | NULL    |                |
| transferId     | varchar(255) | YES  | UNI | NULL    |                |
| status         | int(11)      | NO   |     | NULL    |                |
| updatedAt      | datetime     | NO   |     | NULL    |                |
| paymentVoucher | varchar(255) | NO   |     | NULL    |                |

This section describes how to install the **HiPay Wallet cash-out integration for Mirakl** using [Composer](https://getcomposer.org/), the PHP package manager. The software being installed is based on the [Silex PHP micro-framework](http://silex.sensiolabs.org/).

1. Connect to your web server using SSH

2. Go in your web projects directory (example: `$ cd /var/www` or `$ cd /srv`)
	
5. Download and install Composer (if you haven't already done so): 

	`$ curl -sS https://getcomposer.org/installer | php -- --filename=composer -- --install-dir=/usr/local/bin`
	
6. Create the project using the Composer `create-project` command: 

	`$ composer create-project hipay/hipay-wallet-cashout-mirakl-integration hipay_mirakl` 
	
	This step may take a few minutes to complete as the project and its dependencies are being downloaded and configured.
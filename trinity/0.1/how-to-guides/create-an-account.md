# Create an account

**Trinity accounts are password-protected to secure and store your seeds on your mobile device or computer.**

1. [Download and install Trinity](https://trinity.iota.org/)

2. Open Trinity

3. To create a seed in Trinity, click **Yes, I need a seed**. If you already have a seed, or if you created a seed outside of Trinity, click **No, I have one**.
    
    :::info:
    If you have a [hardware wallet](../concepts/hardware-wallet.md), connect it and follow the on-screen instructions. You don't need to back up your seed if you use a hardware wallet.
    :::
   
    ![Generating a seed](../images/seed-generation.png)

4. Enter an account name for your seed

    :::info:
    You can choose to rename your account later in the [Account management](../how-to-guides/manage-your-account.md).
    :::

    ![Account name](../images/account-name.jpg)

5. Select an option to back up your seed and enter a login password. You will need this password every time you log into Trinity.

    :::info:
    You can choose to add extra account security in the [Security settings](../how-to-guides/manage-your-security-settings.md)
    :::

## Back up your seed

Your seed is your secret password, which is used to generate unique addresses and digital signatures. Addresses are the accounts from which transactions are sent and received. Digital signatures prove ownership of an account and allow value transactions to be sent from addresses.

Trinity secures and stores your seed on your mobile device or computer. Therefore, if you were to ever lose your mobile device or computer, your seeds would be lost. To avoid losing your seed (and your IOTA tokens), you must back it up and keep the backup in a safe place.

:::danger:Important
Anyone who has access to your seed has access to your funds. Do not screenshot your seed.
:::

You must choose one of the following options to back up your seed:
* SeedVault file (most secure)
* Paper copy
* Printed copy (least secure)

After backing up your seed, Trinity asks you to re-enter your seed to make sure that you backed up the correct one.

### Export your seed as a SeedVault file

Exporting your seed to a SeedVault file is the most secure option (apart from using a [hardware wallet](../concepts/hardware-wallet.md)).  

SeedVault is a password-encrypted file that uses the [kdbx file format](https://keepass.info/help/kb/kdbx_4.html). This format is also used by the [KeePass](https://keepass.info/) password manager.

You can export and store your seed in SeedVault or in the KeePass password manager, and use it to log into Trinity when necessary. 

### Write your seed on a piece of paper

Write your seed from left to right, top to bottom. **Check that your seed is written correctly.**

Make sure to write your seed's 3-letter checksum and keep it separate from your seed. This checksum is a safety mechanism that allows you to check whether you entered the correct seed. If you enter one wrong character, the checksum that's displayed in Trinity will be different.

### Print your seed

Although printing your seed is convenient, it can be unsafe. If you're unsure about security, then use another option to back up your seed. 

:::danger:important
* Never print your seed on PDF file.
* Never print your seed from a public printer or a WiFi printer.
:::

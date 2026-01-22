# Active Directory Tutorial: Account Lockouts, Account Management, and Logs

## Overview

This tutorial walks through how to **simulate account lockouts**, **configure Group Policy**, **unlock and reset accounts**, **enable and disable user accounts**, and **observe logs** on a Domain Controller.

---

## Part 1: Simulating an Account Lockout


### Step 1: Log into the Domain Controller

1. Log into **DC-1** using a Domain Admin account.

### Step 2: Choose a User Account

1. Open **Active Directory Users and Computers (ADUC)**.
2. Select a **random user account** that you previously created (for example: a standard employee account).

### Step 3: Trigger Failed Login Attempts

1. Log out of the Domain Controller or open a separate login session.
2. Attempt to log in using the selected user account.
3. Enter an **incorrect password** **10 times**.

> At this stage, the account should not yet be locked if account lockout policies are not configured.

---

## Part 2: Configuring Account Lockout Policy (Group Policy)


### Step 4: Open Group Policy Management

1. On **DC-1**, open **Group Policy Management**.
2. Expand your domain (e.g., `mydomain.com`).
3. Right-click **Default Domain Policy** and select **Edit**.

### Step 5: Configure Account Lockout Threshold

Navigate to:

```
Computer Configuration
└── Policies
    └── Windows Settings
        └── Security Settings
            └── Account Policies
                └── Account Lockout Policy
```

Configure the following:

* **Account lockout threshold**: `5 invalid logon attempts`
* When prompted, allow Windows to automatically configure:

  * **Account lockout duration**
  * **Reset account lockout counter after**

Close the Group Policy Editor.

### Step 6: Apply Group Policy

1. Open **Command Prompt** as Administrator.
2. Run: `gpupdate /force`

---

## Part 3: Confirming Account Lockout

### Step 7: Trigger the Lockout

1. Attempt to log in with the same user account.
2. Enter an **incorrect password 6 times**.

### Step 8: Verify the Account is Locked

1. Open **Active Directory Users and Computers**.
2. Locate the user account.
3. Open **Properties** → **Account** tab.
4. Observe that the account is **locked out**.

---

## Part 4: Unlocking and Resetting the Account

### Step 9: Unlock the Account

1. In the user’s **Account** tab:

   * Check **Unlock account**
   * Click **Apply**

### Step 10: Reset the Password

1. Right-click the user account.
2. Select **Reset Password**.
3. Set a new password.

### Step 11: Test Login

1. Attempt to log in using the user account.
2. Verify that login is **successful** with the new password.

---

## Part 5: Enabling and Disabling Accounts

### Step 12: Disable the Account

1. In **ADUC**, right-click the same user account.
2. Select **Disable Account**.

### Step 13: Attempt Login (Disabled Account)

1. Try logging in with the disabled account.
2. Observe the error message indicating the account is disabled.

### Step 14: Re-enable the Account

1. Right-click the user account.
2. Select **Enable Account**.

### Step 15: Test Login Again

1. Log in using the re-enabled account.
2. Confirm successful authentication.

---

## Part 6: Observing Logs on the Domain Controller

### Step 16: Open Event Viewer

1. On **DC-1**, open **Event Viewer**.

### Step 17: Review Security Logs

Navigate to:

```
Event Viewer
└── Windows Logs
    └── Security
```

Look for events related to:

* **Failed logon attempts**
* **Account lockouts**
* **Account unlocks**
* **Password resets**

Common Event IDs to observe:

* **4625** – Failed logon
* **4740** – Account locked out
* **4724** – Password reset
* **4722 / 4725** – Account enabled / disabled

---

## Conclusion

In this lab, you:

* Simulated account lockouts
* Configured account lockout policies using Group Policy
* Unlocked and reset user accounts
* Disabled and re-enabled accounts
* Observed authentication and security events in Event Viewer

This exercise demonstrates real-world Active Directory account management and security monitoring techniques commonly used by system administrators.

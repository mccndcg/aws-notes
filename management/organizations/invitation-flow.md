# Invitation Flow

#### Scenario Recap

1. **User1** has an existing AWS account.
2. **Company2** creates an **AWS Organization**.
3. Company2 creates a new **account (Acct1)** under their Organization.

***

#### Key Points

1. **AWS Accounts are independent**
   * User1’s personal AWS account is completely separate from Company2’s AWS Organization.
   * You cannot “merge” or automatically bind User1’s personal account to another organization.
2. **Access to Acct1**
   * To give User1 access to **Acct1**, Company2 must **invite User1 as a user via IAM Identity Center (SSO)** or create an IAM user in Acct1.
3.  **Binding Acct1 to User1 via IAM Identity Center**

    Steps:

    1. **IAM Identity Center (SSO) setup**:
       * Company2 has IAM Identity Center enabled.
    2. **Create a user or group** in IAM Identity Center:
       * User1 can either be created directly in IAM Identity Center or synced from a corporate IdP (SAML/AD).
    3. **Assign account and permission set**:
       * Company2 assigns **Acct1** to User1 (or a group User1 belongs to).
       * Company2 selects a **Permission Set** to define User1’s role in Acct1 (e.g., `ReadOnlyAccess` or `AdminAccess`).
    4. **Access via portal**:
       * User1 logs into the **IAM Identity Center access portal**.
       * User1 sees **Acct1** in the portal.
       * User1 selects a **role** corresponding to the permission set.
       * AWS issues **temporary credentials** for that role in Acct1.

{% hint style="warning" %}
why select a role. can multiple roles be set
{% endhint %}

Yes, this is a crucial part of **IAM Identity Center (AWS SSO)**. Let’s break it down carefully.

***

#### Why Users Select a Role

1. **Permission sets become roles in AWS accounts**
   * When you assign a **permission set** to a user/group for an AWS account, AWS **automatically creates an IAM role** in that account corresponding to the permission set.
   * The role defines **what the user can do** in that account (permissions, session duration, etc.).
2. **Role selection allows flexibility**
   * A user may have multiple permission sets assigned for the same account.
   * Each permission set becomes a **distinct role**.
   * When logging in via the **access portal**, the user chooses which role to assume for that session.

***

#### Can Multiple Roles Be Set?

Yes. Examples:

* **Scenario:** User1 is in a “Developers” group. The group has:
  * `ReadOnlyAccess` for **Acct1**
  * `PowerUserAccess` for **Acct1**
* In the **access portal**, User1 sees **Acct1** with **two roles**:
  * `Acct1 – ReadOnlyAccess`
  * `Acct1 – PowerUserAccess`
* **User choice:** Depending on what they want to do, User1 picks a role:
  * Quick read-only checks → select `ReadOnlyAccess`
  * Deploy or modify resources → select `PowerUserAccess`

***

#### Key Points

* **Each role = one permission set in one account**.
* **Multiple roles per account** are possible by assigning multiple permission sets.
* **Temporary credentials** are generated for the role chosen at login; you cannot combine roles for a single session.
* This keeps **least privilege principles** intact — users only get the permissions they explicitly choose.

***

# Identity and Access Management

Controls access to AWS services via policies.

[Cheat Sheet](https://tutorialsdojo.com/aws-cheat-sheet-aws-identity-and-access-management-iam/)

- It is **global**. Does not apply to regions.

- **Root** - the account created when the AWS account is first setup. It has full Admin privileges.

  - Always setup Multifactor Authentication on this account.

- **Access Keys** - a pair of values aused by applications, SKDs, or the AWS-CLI to authenticate to AWS.

  - The access key ID & secret key are used to access AWS through the Command Line or the APIs.

  - These are only available once. If you misplace them, you have to regenerate them. Store them in a safe location.

  - To access the AWS Console, a password is needed.

  - It is possible to create a customized password rotation policy.

## Users

Type of identity suitable for long-term accesss for a known entity.

- When first created, new users have _no_ permissions.

- Only identity that has access keys. They are assigned an Access Key ID & Secret Access Keys at creation.

- A user can only be a member of 10 distinct groups.

- Default max of 10 managed policies per user.

- Users don't have to belong to a group.

## Groups

A way to attach policies to multiple users at one time. collection of IAM users.

- Groups have no credentials.
- Groups only contain users, not other groups.
- Users don't have to belong to a group.

## Roles

Assumed by another identity allowed in the trust policy.

## Policies

A list of statements that match a request to AWS based on their action and resource.

- Statements result in allow or deny.

- Applied to Users, Groups, and Roles.

- Actions - API calls bein attempted

- Policies must be attached to something

## KMS

Key Management Service - managed service that makes it easy for you to create and control the encryption keys used to encrypt your data.

## Directory Service

Provides multiple ways to use Amazon Cloud Directory and Microsoft AD with other AWS services. Directores store information about suers, groups, and devices, and administrators use them to manage access to information and resources.

- **Directory Service AD Connector** - for when companies are using a corporate AD, to make integration easier

# Organizations

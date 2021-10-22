# Identity and Access Management

- Global service
- Root account – created by default. Do **not** share
- Users – people within your organization. Can be grouped
- Groups – only contain users, not other groups
- Users don't have to belong to a group
- Users can belong to multiple groups
- Permissions – users or groups can be assigned JSON documents called policies
- Least Privilege Principle – don't give more permission than a user needs
- Policies applied to groups are applied to all the group's users
- Inline policies – policies applied directly to users
- Policy structure

  1. version
  1. Id
  1. Statement

     - Sid
     - Effect
     - Principle
     - Action
     - Resource
     - Condition

- Passwords

  - You can setup a custom password policy
  - You can allow users to change their own passwords ore set an expiration date
  - You can prevent password reuse
  - You can require Multi-Factor Authentication

- Options to Access AWS

  - AWS Management Console (password + MFA)
  - AWS CLI (access keys)
  - AWS SDK (access keys)

- IAM Roles – used to assign permissions to AWS Services
- IAM Security Tools

  - IAM Credentials Report (account level) – a report that lists all your account's users and the status of their various credentials
  - IAM Access Advisor (user-level) – shows the service permissions granted to a user and when those services were last accessed

## IAM Best Practices

1. Use root account for AWS setup _only_
1. Assign users to groups and assign permissions to groups
1. Create a strong password policy
1. Use and enforce use of MFA
1. Create and use Roles to give permissions to AWS services
1. Use access keys for programmatic access
1. Audit permissions with the IAM Credentials Report

## IAM Shared Responsibility Model

### AWS

1. Infrastructure (global network security)
1. Configuration and vulnerability analysis
1. Compliance validation

### Customer

1. Users, Groups, Roles, Policies management and monitoring
1. Enable MFA on all accounts
1. Rotate all your keys often
1. Use IAM tools to apply appropriate permissions
1. Analyze access patterns and review permissions

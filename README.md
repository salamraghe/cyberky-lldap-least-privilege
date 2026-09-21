# CyberKy / LLDAP Least-Privilege Groups

Hands-on lab, Sep 2026.

Ticket-style least-privilege access in **LLDAP** (CyberKy “IAM LDAP: Create Your First Group Policy”): create a read-tier group, put an analyst in it, keep them out of admin, prove it by signing in as the analyst.

This is **not** Windows AD Group Policy and not the `ad-user-lifecycle` repo. Entra and Okta live in other repos.

## Scope

| # | Item | Dump |
| --- | --- | --- |
| 1 | LLDAP 0.6.2 UI; users **admin**, **analyst1** | Done (21 Sep 2026) |
| 2 | Custom group **soc-tier1-readonly** with member **analyst1** | Done (21 Sep 2026) |
| 3 | Built-in groups present; **lldap_admin** members = **admin** only | Done (21 Sep 2026) |
| 4 | Validation: signed in as **analyst1** | Done (21 Sep 2026) |

## Environment

| Object | Value |
| --- | --- |
| Lab | CyberKy IAM LDAP (LLDAP web UI) |
| App | LLDAP **0.6.2** |
| Lab URL (ephemeral) | `http://172.19.0.3:17170/` |
| Users | **admin**; **analyst1** |
| Custom group | **soc-tier1-readonly** — member **analyst1** |
| Built-in groups | `lldap_admin`, `lldap_password_manager`, `lldap_strict_readonly` |
| Admin group proof | **lldap_admin** members: **admin** only (analyst1 not added) |

## Screenshots (21 Sep 2026 dump)

- [Users: admin + analyst1](screenshots/01-users-admin-analyst1.png)
- [Groups list includes soc-tier1-readonly](screenshots/02-groups-list.png)
- [lldap_admin members: admin only](screenshots/03-lldap-admin-admin-only.png)
- [Signed in as analyst1](screenshots/04-signed-in-as-analyst1.png)
- [soc-tier1-readonly members: analyst1](screenshots/05-soc-tier1-readonly-members.png)

## What was built

- Created user **analyst1** in LLDAP.
- Created security-style group **soc-tier1-readonly** and added **analyst1**.
- Left **lldap_admin** as **admin** only so the analyst stays least-privilege.
- Signed in as **analyst1** to validate the account.

## How to redo it

1. Open the LLDAP UI for the CyberKy lab (version 0.6.2).
2. As **admin**, create user **analyst1**.
3. Create group **soc-tier1-readonly**; add **analyst1** as a member.
4. Open **lldap_admin** and confirm members are **admin** only — do not add analyst1.
5. Sign out; sign in as **analyst1** and capture user details.

## What broke / notes

- Lab IP `172.19.0.3` is ephemeral; treat it as session proof, not a permanent host.
- Desktop clock appears in the OS panel on these shots; screenshots were not watermark-edited.
- No password dialogs were committed.

## Demo walkthrough

1. Show Users: **admin** and **analyst1**.
2. Show Groups: custom **soc-tier1-readonly** next to the built-in LLDAP groups.
3. Open **lldap_admin** — only **admin** is a member (least privilege).
4. Open **soc-tier1-readonly** — **analyst1** is the member.
5. Show the session signed in as **analyst1**.
6. Explain in ticket language: membership drives privilege; the analyst can read what that tier allows and does not get admin unless assigned.

## Own words (from the sitting)

- analyst1 could only read; could not create, move, or update groups.
- No admin authority unless admin assigned access; membership drives privilege.

## Stop there

Okta and CyberArk are other sittings / other repos. Do not invent Windows GPO, Entra, or Okta into this package.

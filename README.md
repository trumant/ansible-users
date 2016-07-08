[![Build Status](https://travis-ci.org/trumant/ansible-users.png)](https://travis-ci.org/trumant/ansible-users)

# Users role

Role to manage users on a system.

## Role configuration

* users_create_homedirs (default: true) - create home directories for new
  users. Set this to false is you manage home directories separately.

## Creating users

Add a users variable containing the list of users to add. A good place to put
this is in `group_vars/all` or `group_vars/groupname` if you only want the
users to be on certain machines.

The following attributes are required for each user:

* username - The user's username.
* ssh-key - This should be a list of ssh keys for the user. Each ssh key
  should be included directly and should have no newlines.

In addition, the following items are optional for each user:

Example:

    ---
    users:
      - username: foo
        ssh_key:
          - "ssh-rsa AAAAA.... foo@machine"
          - "ssh-rsa AAAAB.... foo2@machine"
    users_deleted:
      - username: bar
        name: Bar User
        uid: 1002

## Deleting users

The `users_deleted` variable contains a list of users who should no longer be
in the system, and these will be removed on the next ansible run. The format
is the same as for users to add, but the only required field is `username`.
However, it is recommended that you also keep the `uid` field for reference so
that numeric user ids are not accidentally reused.

# ACPICA

This repository represents the version of [acpica](https://acpica.org/)
that is used as part of
[illumos-joyent](https://github.com/joyent/illumos-joyent). There are
changes here that generally cover our ability to correctly build the
sources in illumos.

## Repository Management

This repository is downstream of the [github acpica
mirror](https://github.com/acpica/acpica/).

To better understand and maintain our differences from acpica we try to
manage branches and tags in a specific fashion. First and foremost, we
mirror the master branch across as this is the primary branch that is
used by ACPICA, there are no other generally used branches.

Anything that is Joyent-specific begins with a `joyent/` prefix and is
constructed in the form of `joyent/<version>` where `<version>`
corresponds to the timestamped ACPICA release. For example
`joyent/20180629` corresponds to the 20180629 release. These branches
will have all of our patches rebased on top of them. When we're done we
will then create a tag in the repo that uses the form
`joyent/v<release>r<branch release num>`. The first release as described
above would be `joyent/v20180629r1`. If we need another release, we
would increment r and it would be tagged as `joyent/v20180629r2`.

When copying these files into illumos-joyent an OS ticket should be
created that clearly states what the version is that we're using.

## Updating illumos

To update ACPI in illumos, the first thing that you should do is make
sure that the master branch for ACPI is up to date.

Next, one should cherry-pick all the appropriate changes from the
existing branches to the next. If additional changes are required, new
commits should be added. If certain patches are no longer required, then
they should not be picked onto the new branch.

Once the code is in place, use the tools/acpica-update script to update
an illumos workspace. If any other changes to illumos are required, then
they should be made in that repo.

Finally, make sure to test the changes thoroughly on a number of
different platforms.

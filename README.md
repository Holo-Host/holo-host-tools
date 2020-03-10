# holo-host-tools

A collection of little tools for making it easier to work with Holo Host.

## Installation (for both commands)

1. Make sure you have Ruby installed.
2. Download the script (see below for links).
3. Make it executable (you can do this in the terminal by typing `chmod +x <name_of_script>.rb`)

## _Warning!!!_

Both of these scripts contain Paul d’Aoust’s personal API keys for their corresponding services. Don’t share them outside the team!

## `holoport-whitelist`

This tool lets you search and manipulate the whitelist from the CloudFlare K/V store. It’s much easier than paging through their horrible UI!

### Usage

* `holoport-whitelist`

    `holoport-whitelist list`

    Just show all the email addresses in the whitelist. The `list` parameter is optional, because this is the default action.

* `holoport-whitelist > whitelist.csv`

    Export the whitelist to a file.

* `holoport-whitelist --malformed-only`

    Only show malformed email addresses (upper-case or invalid characters).

* `holoport-whitelist search email1@example.com email2@example.com`

    `holoport-whitelist search < emails-to-search-for.txt`

    Quickly search the whitelist for one or more email addresses.

* `holoport-whitelist add email1@example.com email2@example.com`

    `holoport-whitelist add < emails-to-add.txt`

    Add one or more email addresses to the whitelist. Does all the cleanup for you, and throws an error for any emails it can’t clean up.

* `holoport-whitelist remove bad-email@example.com`

    Remove an email address (and all the malformed variants it can find) from the whitelist.

* `holoport-whitelist autofix`

    Looks for all malformed emails and tries to fix them. If an email is too malformed, it’ll skip it.

#### Parameters

* `--token <token>`

    `-t <token>`

    The CloudFlare authorization token to use for this call. Must have access to Holo's K/V store, and must have write access if adding, removing, or autofixing entries. If you don't have one, please talk to Holo TechOps.

* `--account <account_id>`

    `-a <account_id>`

    The ID of Holo's CloudFlare account that holds the whitelist. If you don't know it, please talk to Holo TechOps.

* `--namespace <namespace_id>`

    `-n <namespace_id>`

    The ID of the CloudFlare namespace that holds the whitelist. If you don't know it, please talk to Holo TechOps.

* `--malformed-only`

    `-m`

    Only operate on malformed emails in the whitelist. Valid for `list`, `search`, and `remove` actions.

* `--no-format`

    Most of the time malformed email addresses are highlighted to show their invalid characters and whether a properly formed variant exists in the whitelist. This turns that off. Valid for `list` (but only when `--malformed-only` is also specified), `search`, `remove`, and `autofix`.

* `--accept`

    `-y`

    Say yes to every change instead of prompting.

* `--dry-run`

    `-n`

    Say no to every change instead of prompting. Show what would be changed.

#### Environment variables

Put these variables into your `.profile` or `.bash_profile` file and you'll never have to specify them as flags.

* `HOLO_WHITELIST_CLOUDFLARE_TOKEN`

    Your CloudFlare API token. See the `--token` command-line flag for details.

* `HOLOPORT_WHITELIST_CLOUDFLARE_ACCOUNT`

    The ID of Holo's CloudFlare account. See the `--account` comand-line parameter for more details.

* `HOLOPORT_WHITELIST_CLOUDFLARE_NAMESPACE`

    The ID of the CloudFlare namespace that holds the namespace. See the `--namespace` command-line parameter for more details.

## `zerotier-members-list`

This tool lets you get the email addresses of all currently registered HoloPort owners. The ZeroTier UI is decent, but this is useful for exporting to a different service, like a mail campaign. Like `holoport-whitelist`, it outputs each email address on its own line.

### Usage

* `zerotier-members-list > registered-holoports.csv`

    Export the list to a file.

* `zerotier-members-list | grep -i email_address@example.com`

    Quickly search the members list for a single email address.

### Parameters

* `--token <token>`

    `-t <token>`

    The CloudFlare API token to use for this call. Must have access to Holo's K/V store, and must have write access if adding, removing, or autofixing entries. If you don't have one, please talk to Holo TechOps.

* `--network <network_id>`

    `-n <network_id>`

    The ID of the ZeroTier network that contains the HoloPorts. If you don't know it, you can get it from the TechOps team.

### Environment variables

* `HOLO_ZEROTIER_TOKEN`

    The ZeroTier authorization token. See the `--token` command-line parameter for more details.

* `HOLO_ZEROTIER_NETWORK`

    The ID of the HoloPort ZeroTier network. See the `--network` command-line parameter for more details.
assume_role.sh
==============

This is a simple script to assume IAM roles on your command line. The script is written in pure shell, without any dependencies.

Installation
------------

Copy `assume_role.sh` somewhere (e.g. by checking out this repository) and source it in your shell's initialization script
(e.g. `.bashrc` or `.zshrc`):
```
source <path to repo>/assume_role.sh
```

Usage
-----

The script will add two functions `assumerole` and `leaverole` that can be used as follows:
```
assumerole dev
```
This command checks `~/.aws/config` for a profile called `dev` and tries to assume the corresponding role.
Alternatively, you can specify the ARN of the role (without using `~/.aws/config`):
```
assumerole arn:aws:iam:...
```

Optionally, you can specify a session name:
```
assumerole dev "Testing feature xyz"
```

The `assumerole` function works by setting various environment variables (e.g. `AWS_ACCESS_KEY_ID`) that are generally
recognized by all command line tools for AWS.

To leave the role (i.e. unsetting the environment variables) simply call `leaverole`.

Calling `assumerole` without arguments prints the name of the currently assumed role.

Of course, `assumerole` requires that your current profile (generally the default profile) is allowed to assume the given role.

Configuration
-------------
Unless you specify complete ARNs, `assumerole` requires that you define role names as profiles in `~/.aws/config`. For example:
```
[profile dev]
role_arn=arn:aws:iam:...
region=eu-central-1
```
See [Configuration and Credential Files](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html) in the AWS docs for more information.

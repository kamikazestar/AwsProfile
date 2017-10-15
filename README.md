# AwsProfile

Simple Bash script used to switch between many different AWS profiles in easy and fast way.

## Getting started

This is simple bash script so it's not require any build process.

### Prerequisites and assumptions

To use this tool you need to firstly install awscli via pip. All details how to do that
are available [here](http://docs.aws.amazon.com/cli/latest/userguide/installing.html).
To be able to use awscli you need to add directory where was placed to PATH variable.
You can check where awscli had been placed using this command:

```
whereis aws
```

Then you can add that to your PATH variable in ~/.profile file:

```
if [ -d "$HOME/.local/bin" ] ; then
    PATH="$HOME/.local/bin:$PATH"
fi
```

That's something which is specific for my system so be careful with coping that directly.
After awscli installation we need to configure two files located in ~/.aws directory, one
of them is config and second one is credentials. Here I made some assumptions that are important
form security point of view. I decided that safer is to don't have default profile configured
and set that on-purpose instead working on some default profile by default. Because of that I
configured my ~/.aws/config in this way:

```
[profile Profile1]
region=eu-west-1
output = table

[profile Profile2]
region=eu-central-1
output = text

...
```

As you can see there's no default profile. Configuration of ~/.aws/credentials file is similar:

```
[Profile1]
aws_access_key_id=[here_is_my_access_key_id_to_profile1]
aws_secret_access_key=[here_is_my_secret_key_to_profile1]

[Profile2]
aws_access_key_id=[here_is_my_access_key_id_to_profile2]
aws_secret_access_key=[here_is_my_secret_key_to_profile2]

...
```

### Installation and configuration

On daily basis I work on Ubuntu operating system, so by default PATH variable is set to
~/bin directory, but not in my case. I changed that to ~/.bin so please remember abut that
when you will be copying file to your ~/.bin directory:

```
# set PATH so it includes user's private bin if it exists
#if [ -d "$HOME/bin" ] ; then
#    PATH="$HOME/bin:$PATH"
#fi
if [ -d "$HOME/.bin" ] ; then
    PATH="$HOME/.bin:$PATH"
fi
```

So in my case I placed script in ~/.bin directory, but this can be different in your case.
To be able to pass variables to your current shell you need to add alias for aws-profile command.
By default Ubuntu is including file ~/.bash_aliases:

```
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

Because of that I added this line to my ~/.bash_aliases file:

```
# AWS
alias aws-profile="source aws-profile"
```

Command completions for awscli is available, details are availabe [here](http://docs.aws.amazon.com/cli/latest/userguide/cli-command-completion.html)
To be able to use this functionality I added this code to my ~/.bashrc file:

```
# enable aws-cli completion feature.
if [ -f ~/.local/bin/aws_completer ]; then
        complete -C '~/.local/bin/aws_completer' aws
fi
```

I also decided to add some custom field to bash prompt to always know on which profile
I currently work:

```
PS1='${debian_chroot:+($debian_chroot)}\[\033[38;5;028m\]\u\[\033[38;5;001m\]@\h\[\033[00m\]: \[\033[38;5;003m\]($AWS_PROFILE) \[\033[38;5;025
m\]\w\[\033[00m\]\$ '
```

## Versioning and branching

This is initial and working version of the script so I decided to version that as
version 0.1.0.

This is very small project, but like in other cases I will follow Git successful
branching model. More details available [here](http://nvie.com/posts/a-successful-git-branching-model/)

## Authors

Initial work: [Marcin Słaboński](slabonski.marcin+git@gmail.com)

## Acknowledgments

Below I placed some articles that inspired me to wrote this script:

- [aws-profile](https://github.com/jaymecd/aws-profile) project of [Nikolai Zujev](https://github.com/jaymecd)
- [completion](http://mads-hartmann.com/2017/04/27/multiple-aws-profiles.html) by [Mads Hartmann](https://github.com/mads-hartmann)
- [completion](https://www.isc.upenn.edu/using-bash-auto-completion-easily-switch-between-aws-accounts) by Michel van der List

## License

I'm using FOSS software on daily basics so this project is also licensed on MIT license, but I not taking any responsibility
for results of using this software.

## TODO

- AWS profile completion

How to use nested variables
===========================

This how to will briefly describe how you can create a variable name which is comprised of embedded or nested variables which Ansible will recognize.

So what is a nested variable anyway?
------------------------------------

Simply put a nested variable is a varible whose value is made up of multiple levels of variable values.  Oh wait maybe not so simple.  Let's take a look at an example.  That always helps.

Example
-------

Example vault file snippet(s) decoded:

```text/x-yaml

#
# (Development Environment)
#
vault_development_password: "SuperPrivateDevelopmentPassword"

#
# (Development Environment)
#
vault_production_password: "SuperPrivateProductionPassword"

```

The snippets above depict an example decoded vault file which contains lifecycle specific variable(s).


 Example vars file snippet:

```text/x-yaml

environment: "development"

username: "fwondergums"
password: "{{ lookup('vars', 'vault_' + environment + '_password') }}"

```

In the vars file snippet above we see that depending upon the value assigned to the "environment" variable the password variable should have a lifecycle specific value assigned to it.

Food for thought
----------------

Ansible does not allow you to use multiple layers of braces/mustaches/etc to decode variables.  You must rely on your Jinja2 ninja skills and create the variable name using concatenation.

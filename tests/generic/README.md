# Generic

These tests provide generic Zimbra supported protocol performance testing.

All these tests depend on the Zimbra JMeter Library zjmeter.jar and assume no SSL usage.

The following protocols currently have a basic level of support:

* smtp
  
  [Simple Mail Transfer Protocol](https://tools.ietf.org/html/rfc5321) view [smtp](smtp/smtp.md) for a list of currently supported commands in the jmx.
  
* lmtp
  
  [Local Mail Transfer Protocol](https://tools.ietf.org/html/rfc2033) view [lmtp](lmtp/lmtp.md) for a list of currently supported commands in the jmx.
  
* imap
  
  [Internet Message Access Protocol](https://tools.ietf.org/html/rfc3501) view [imap](imap/imap.md) for a list of currently supported commands in the jmx.
  
* pop
  
  [Post Office Protocol](https://tools.ietf.org/html/rfc5321) view [pop](pop/pop.md) for a list of currently supported commands in the jmx.
  
* zsoap
  
  [Zimbra SOAP API](https://wiki.zimbra.com/wiki/SOAP_API_Reference_Material_Beginning_with_ZCS_8) view [zsoap](zsoap/zsoap.md) for list of currently supported commands in the jmx.

This directory also contains a test mix this jmx combines all the above tests into one jmx file that can be used for very low combined user count tests.

# Example

Any of these tests can be used following this basic outline of steps:

```
# grab a copy of the tests
$ get clone https://github.com/Zimbra/zm-load-testing.git 
$ cd zm-load-testing

# create a user.csv file of accounts that can be used for testing
# <user>,<password>
# add as many users as you want to test with
$ vi /tmp/users.csv
user1,userpass
...

# create zimbra environment specific property file for desired test example zsoap
$ cp tests/generic/zsoap/env.prop /tmp/myenv.prop
$ vi /tmp/myenv.prop
modify file appropriately for the zimbra environment you plan to test
update the users.csv file to the csv file created above

# run the predifined load and basic profile without using the GUI
# note: some property files use relative paths that assume jmeter is run from the repo's top directory
$ jmeter -n -q /tmp/myenv.prop -q tests/generic/zsoap/load.prop -q tests/generic/zsoap/profile/basic.prop -t tests/generic/zsoap/zsoap.jmx
```

The default load.prop file for all the tests is a single user that runs the specified profile once then exits. Just as you created a custom env.prop you can copy the load.prop file to adjust load as desired.

The same also works for creating custom profiles for these generic tests. The generic tests ideally would support all the protocol defined commands however at this time the jmx files only support a subset of any particular protocols commands. The profile allows you to define any sequence of the available commands to execute.
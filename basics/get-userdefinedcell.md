# Close Visio applications

While you are writing scripts to automate Visio, at some point you'll be running script over and over and you'll notice you've created many instances of Visio. Stopping them manually can take some time. Fortunately you can quickly kill them by running the following command.

```text
Stop-Process -name "Visio"
```

This cmdlet will have an error if there are no Visio applications open. So you can handle that case with this command:

```text
stop-process -name visio -ErrorAction ignore
```


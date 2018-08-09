# commands-chainer

> DSL to create a chain of commands.

> The CommandExecutor class take in charge the command creation and execution.

> The CommandsChainGuard allows you to enable/disable a flow of commands.


1) Execute commands
```
        CommandsChain
                .create()
                .using(executor)
                    .command(TestCommand1.class)
                    .command(TestCommand2.class)
                .execute();

```

2) Execute child commands with guard
```
        CommandsChain
                .create()
                .using(executor)
                    .command(TestCommand1.class)
                    .on(guard)
                       .cildCommand(TestCommand2.class)
                    .endOn()
                    .command(TestCommand3.class)
                .execute();

```
the TestCommand2 will be executed only if guard callback return true.


3) Execute recursive child commands with guard
```
        CommandsChain
                .create()
                .using(executor)
                    .command(TestCommand1.class)
                    .on(guard)
                       .cildCommand(TestCommand2.class)
                       .onChild(childGuard)
                           .cildCommand(TestCommand3.class)
                       .endChild()
                    .endOn()
                    .command(TestCommand4.class)
                .execute();
```

the TestCommand3 will be executed only if guard and childGuard callbacks returns true.


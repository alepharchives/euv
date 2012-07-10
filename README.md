euv
===

These are Erlang bindings to libuv. There goals for this project are to
create a stable binding to libuv's file handling and demonstrate how that
affects file IO for processes with large mailboxes.

If that work goes quickly enough I'll add wrappers to the networking parts
of libuv and lastly if time I'll add the HTTP parser from node and compare
that against Erlang's builtin HTTP packet parsing.

Current Status
--------------

While this NIF works well enough to do basic open/read/write/close file
IO (on OS X at least) I've completely missed the mark on my original goals of relying on the OTP-8623 optimization for message passing with newly created
references. Ie, its no better (and I think a tidge slower) than the builtin
file module. If/when I figure out how to make that selective receive more
efficient for messages generated from a NIF we can look into rebooting this
project.

Building and Testing
--------------------

Theoretically you should be able to build this on OS X by just running
`make` in the top directory.

The tests I was using are:

    $ ./test/example-problem.es
    $ ERL_FLAGS="-pa ebin" ./test/example-using-euv.es

The fact that they both follow the same latency curves shows that
my NIF isn't nearly as awesome as I had hoped it would be.

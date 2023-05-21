# Layers

When a command is executed in a terminal, what might be perceived as a simple action is actually the culmination of many complex processes involving several layers of abstraction within the computer system. This process ultimately leads to the command being executed by the computer hardware.

But let's take a step back to look at these layers, starting from the bottom up, and see how they interact with each other to make the command execution possible.

The general idea is that you start with the services offered by the underlying hardware and then add a sequence of layers, each providing a higher (more abstract) level of service. The services provided at the high layers are implemented in terms of the services provided by the low layers.

##

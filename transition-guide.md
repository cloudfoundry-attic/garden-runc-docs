# Transitioning from Garden-Linux

## Behaviour differences

Garden-Linux and Garden-RunC are entirely compatible at the Garden API level,
and have almost identical behaviour (exceptions to that described below).

With garden-runc, a process is considered to have exited only after garden has
been able to collect all the output from all the processes to which it has
attached output streams. This is different from garden-linux, which does not
wait, and means that some processes that were cancellable in garden-linux may
cancel more slowly or not at all with garden-runc.

Garden-Linux always required the `User` field in any `garden.ProcessSpec` to be
specified. In Garden-RunC, the `User` field is optional and if not specified
will default to `root`. This should make no difference in the CF/Diego use case,
where the user is always specified.

## BOSH properties

This guide assumes that you are transitioning from [Garden-Linux-Release
v0.337.0](https://github.com/cloudfoundry-incubator/garden-linux-release/releases/tag/v0.337.0),
and is currently up to date with respect to [Garden-RunC-Release
v0.2.0](https://github.com/cloudfoundry-incubator/garden-runc-release/releases/tag/v0.2.0).

Most properties are identical and should not need to be changed when replacing
Garden-Linux with Garden-RunC.

The following properties have default values in Garden-RunC and Garden-Linux:

- `max_containers`: default is 250 in Garden-Linux, but it has no default in
  Garden-RunC - this will be rectified in Garden-RunC v0.3.0
- `log_level`: default is `info` in Garden-RunC, but it has no default in
  Garden-Linux - the behaviour is the same though, as the internal default for
  Garden-Linux when no log level is specified is also `info`

The following properties from Garden-Linux have not yet been implemented for
Garden-RunC:

- `http_proxy`
- `https_proxy`
- `no_proxy`

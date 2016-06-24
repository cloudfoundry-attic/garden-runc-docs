# Container Lifecycle

Garden manages the entire lifecycle of containers. The API allows users to
create, configure, use, and destroy containers.

## Create

Every container is identified by its handle, which Garden returns upon creating
it if it is not provided by the client. In Cloud Foundry, container handles are
specified by the Diego scheduler and provided as part of the container creation
request.

Once a container is created it is immediately ready for use. All resources will
be allocated, the necessary processes will be started and all firewalling tables
will have been updated.

## Use

The container can be used by running arbitrary processes inside it, copying
files in and out, and modifying firewall rules. See the
[`Container`](https://godoc.org/github.com/cloudfoundry-incubator/garden#Container)
interface for a complete list of operations.

## Destroy

When a container is destroyed, Garden invokes the `runc kill` command for that
container. This command sends the `KILL` signal to the init process of the
container. The linux kernel guarantees that all processes in the container
process tree will be killed as a result of this. Once all resources the
container used have been released, its files are removed and it is considered
destroyed.


# Transitioning from Garden-Linux

## Behaviour differences

Garden-Linux and Garden-RunC are entirely compatible at the Garden API level,
and have almost identical behaviour (exceptions to that described below).

Garden-Linux always required the `User` field in any `garden.ProcessSpec` to be
specified. In Garden-RunC, the `User` field is optional and if not specified
will default to `root`. This should make no difference in the CF/Diego use case,
where the user is always specified.

## BOSH properties

This guide assumes that you are transitioning from [Garden-Linux-Release
v0.337.0](https://github.com/cloudfoundry-incubator/garden-linux-release/releases/tag/v0.337.0).

The following properties are identical and should not need to be changed when
replacing Garden-Linux with Garden-RunC:

- `allow_host_access`
- `allow_networks`
- `debug_listen_address`
- `default_container_grace_time`
- `default_container_rootfs`
- `deny_networks`
- `destroy_containers_on_start`
- `dns_servers`
- `docker_registry_endpoint`
- `dropsonde.destination`
- `dropsonde.origin`
- `graph_cleanup_threshold_in_mb`
- `insecure_docker_registry_list`
- `listen_address`
- `listen_network`
- `log_level`
- `max_containers`
- `network_mtu`
- `persistent_image_list`
- `port_pool.size`
- `port_pool.start`

The following properties from Garden-Linux have not yet been implemented for
Garden-RunC:

- `http_proxy`
- `https_proxy`
- `network_pool`
- `no_proxy`

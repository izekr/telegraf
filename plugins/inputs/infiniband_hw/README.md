# InfiniBand Hardware Input Plugin

This plugin gathers statistics for all InfiniBand devices and ports on the
system. These are the hardware counters that can be found in
`/sys/class/infiniband/<dev>/ports/<port>/hw_counters/`

**Supported Platforms**: Linux

## Global configuration options <!-- @/docs/includes/plugin_config.md -->

In addition to the plugin-specific configuration settings, plugins support
additional global and plugin configuration settings. These settings are used to
modify metrics, tags, and field or create aliases and configure ordering, etc.
See the [CONFIGURATION.md][CONFIGURATION.md] for more details.

[CONFIGURATION.md]: ../../../docs/CONFIGURATION.md#plugins

## Configuration

```toml @sample.conf
# Gets hardware counters from all InfiniBand cards and ports installed
# This plugin ONLY supports Linux
[[inputs.infiniband_hw]]
  # no configuration
```

## Metrics

Actual metrics depend on the InfiniBand devices, the plugin uses a simple
mapping from hw_counter -> hw_counter value.

[Information about the hw_counters][hw_counters] collected is provided by Mellanox.

[hw_counters]: https://enterprise-support.nvidia.com/s/article/understanding-mlx5-linux-counters-and-status-parameters

- infiniband
  - tags:
    - device
    - port
  - fields:
    - duplicate_request (integer)
    - implied_nak_seq_err (integer)
    - lifespan (integer)
    - local_ack_timeout_err (integer)
    - np_cnp_sent (integer)
    - np_ecn_marked_roce_packets (integer)
    - out_of_buffer (integer)
    - out_of_sequence (integer)
    - packet_seq_err (integer)
    - req_cqe_error (integer)
    - req_cqe_flush_error (integer)
    - req_remote_access_errors (integer)
    - req_remote_invalid_request (integer)
    - resp_cqe_error (integer)
    - resp_cqe_flush_error (integer)
    - resp_local_length_error (integer)
    - resp_remote_access_errors (integer)
    - rnr_nak_retry_err (integer)
    - roce_adp_retrans (integer)
    - roce_adp_retrans_to (integer)
    - roce_slow_restart (integer)
    - roce_slow_restart_cnps (integer)
    - roce_slow_restart_trans (integer)
    - rp_cnp_handled (integer)
    - rp_cnp_ignored (integer)
    - rx_atomic_requests (integer)
    - rx_icrc_encapsulated (integer)
    - rx_read_requests (integer)
    - rx_write_requests (integer)

## Example Output

```text
infiniband,device=mlx5_0,port=1 VL15_dropped=0i,excessive_buffer_overrun_errors=0i,link_downed=0i,link_error_recovery=0i,local_link_integrity_errors=0i,multicast_rcv_packets=0i,multicast_xmit_packets=0i,port_rcv_constraint_errors=0i,port_rcv_data=237159415345822i,port_rcv_errors=0i,port_rcv_packets=801977655075i,port_rcv_remote_physical_errors=0i,port_rcv_switch_relay_errors=0i,port_xmit_constraint_errors=0i,port_xmit_data=238334949937759i,port_xmit_discards=0i,port_xmit_packets=803162651391i,port_xmit_wait=4294967295i,symbol_error=0i,unicast_rcv_packets=801977655075i,unicast_xmit_packets=803162651391i 1573125558000000000
```

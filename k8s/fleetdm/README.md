# Fleet Device Management

Fleet Device Management is a free and open source device management solution for teams of any size. It supports all major operating systems, while still allowing low-level access to OS-specific features.

- [Documentation](https://fleetdm.com/docs/)
- [Helm Chart](https://github.com/fleetdm/fleet/tree/main/charts/fleet)

## Dependencies

- [MySQL](../mysql)

## Post-build variables

| Variable               | Description                                         | Default | Required |
| ---------------------- | --------------------------------------------------- | :-----: | :------: |
| fleetdm_mysql_password | The password for the MySQL database used by FleetDM | fleetdm |    ✕     |
| fleetdm_redis_password | The password for the Redis database used by FleetDM | fleetdm |    ✕     |

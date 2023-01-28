# Services
Services are deamons that run in the background. This are usually servers to offer services like a database. When this are installed install script to be adminstrated by systemclt. But in light systems like containers and WSL (Windows Subsystem for Linux) this command doesn't exist. Can be installed but this bloated the images and this makes no sense with light weight system definition.

But fortunately this the services can be started by it's own script manually. All services are under `/etc/init.d` and can be listed with `services --status-all`. This command gives us the list and status with all the options like `start`, `stop`, `restart`, etc.

To start service manually we only need to:
```bash
/etc/init.d/<service name> start
```

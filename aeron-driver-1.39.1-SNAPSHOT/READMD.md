#### Mac/Darwin

Mac tends to use `SO_SNDBUF` values that are too small. It is recommended to use larger values, like 16KB.

**Note:** Since Mac OS does not have a built-in support for `/dev/shm` it is advised to create a RAM disk for the Aeron directory (`aeron.dir`).

You can create a RAM disk with the following command:
```shell
$ diskutil erasevolume HFS+ "DISK_NAME" `hdiutil attach -nomount ram://$((2048 * SIZE_IN_MB))`
```
where:
- `DISK_NAME` should be replaced with a name of your choice.
- `SIZE_IN_MB` is the size in megabytes for the disk (e.g. `4096` for a `4GB` disk).

For example, the following command creates a RAM disk named `DevShm` which is `2GB` in size:
```shell
$ diskutil erasevolume HFS+ "DevShm" `hdiutil attach -nomount ram://$((2048 * 2048))`
```
After this command is executed the new disk will be mounted under `/Volumes/DevShm`.


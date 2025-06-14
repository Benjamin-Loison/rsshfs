`rsshfs` (reverse `sshfs`) allows to mount a local folder to a remote host
using `sshfs`.

See <https://blog.rom1v.com/2014/06/sshfs-inverse-rsshfs/>.

## Dependencies

On the local host:

 * `openssh-sftp-server`

On the remote host:

 * `sshfs`
 * `fuse`

The user on the remote host must be in the group `fuse`:

~~~shell
addgroup "$USER" fuse  # and reconnect the session
~~~

## Mount a folder

`sshfs` can mount a remote folder to a local one:

~~~
sshfs server:/remote/folder /local/folder
~~~

In the same way, `rsshfs` can mount a local folder to a remote one:

~~~
./rsshfs /local/folder server:/remote/folder
~~~

It is possible to mount it in *read-only* mode:

~~~
./rsshfs /local/folder server:/remote/folder -o ro
~~~

Contrary to `sshfs`, as `rsshfs` acts as a server, it does not return until the
remote folder is unmounted.

## Unmount

For unmounting:

~~~
./rsshfs -u server:/remote/folder
~~~

It should make the mounting command finish.

Or more simply, by pressing `Ctrl+C` in the terminal of the mount command.

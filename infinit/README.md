<!--

********************************************************************************

WARNING:

    DO NOT EDIT "infinit/README.md"

    IT IS AUTO-GENERATED

    (from the other files in "infinit/" combined with a set of templates)

********************************************************************************

-->

# Supported tags and respective `Dockerfile` links

-	[`0.7.3-debian` (*0.7.3/debian/Dockerfile*)](https://github.com/infinit/infinit-docker/blob/67fc4ba5a08895844ccdd508133479cf4ab0e9a7/0.7.3/debian/Dockerfile)
-	[`0.7.3-alpine`, `0.7.3` (*0.7.3/alpine/Dockerfile*)](https://github.com/infinit/infinit-docker/blob/67fc4ba5a08895844ccdd508133479cf4ab0e9a7/0.7.3/alpine/Dockerfile)
-	[`0.8.0-debian` (*0.8.0/debian/Dockerfile*)](https://github.com/infinit/infinit-docker/blob/67fc4ba5a08895844ccdd508133479cf4ab0e9a7/0.8.0/debian/Dockerfile)
-	[`0.8.0-alpine`, `0.8.0`, `latest` (*0.8.0/alpine/Dockerfile*)](https://github.com/infinit/infinit-docker/blob/67fc4ba5a08895844ccdd508133479cf4ab0e9a7/0.8.0/alpine/Dockerfile)

# Quick reference

-	**Where to get help**:  
	[the Docker Community Forums](https://forums.docker.com/), [the Docker Community Slack](https://blog.docker.com/2016/11/introducing-docker-community-directory-docker-community-slack/), or [Stack Overflow](https://stackoverflow.com/search?tab=newest&q=docker)

-	**Where to file issues**:  
	[https://github.com/infinit/infinit-docker/issues](https://github.com/infinit/infinit-docker/issues)

-	**Maintained by**:  
	[Infinit](https://github.com/infinit/infinit-docker)

-	**Published image artifact details**:  
	[repo-info repo's `repos/infinit/` directory](https://github.com/docker-library/repo-info/blob/master/repos/infinit) ([history](https://github.com/docker-library/repo-info/commits/master/repos/infinit))  
	(image metadata, transfer size, etc)

-	**Image updates**:  
	[official-images PRs with label `library/infinit`](https://github.com/docker-library/official-images/pulls?q=label%3Alibrary%2Finfinit)  
	[official-images repo's `library/infinit` file](https://github.com/docker-library/official-images/blob/master/library/infinit) ([history](https://github.com/docker-library/official-images/commits/master/library/infinit))

-	**Source of this description**:  
	[docs repo's `infinit/` directory](https://github.com/docker-library/docs/tree/master/infinit) ([history](https://github.com/docker-library/docs/commits/master/infinit))

-	**Supported Docker versions**:  
	[the latest release](https://github.com/docker/docker/releases/latest) (down to 1.6 on a best-effort basis)

# What is Infinit?

Infinit’s storage platform transforms commodity servers into multiple flexible, scalable, secure and fault-tolerant storage logics tailored to your applications.

![logo](https://raw.githubusercontent.com/docker-library/docs/fcf56dc19ac54b6e5a2763f07501f9a2e2c715c3/infinit/logo.png)

# How to use this image?

The following commands show Docker-specific tips for a pleasant integration between Infinit and Docker. For the Infinit-specific documentation, consult [Infinit's website](https://infinit.sh/get-started).

## Basics

	docker run --rm infinit

### Sharing configuration folder

Infinit stores its configuration under `/root/.local/share/infinit`. If you want to share this folder with your host, you can mount your host's configuration folder as a volume in your container.

	docker run -v ~/.local/share/infinit:/root/.local/share/infinit --rm infinit

*N.B. This might affect permissions of the mounted folder.*

### Using your user

By default, Infinit uses the current user, `root` when running on a container. If you want to use your local user name, you can set the INFINIT_USER environment variable.

	docker run -e INFINIT_USER=$USER -v ~/.local/share/infinit:/root/.local/share/infinit --rm infinit

### Accessing storage logics

For now, the only logic available is a distributed file system.

#### File system

On UNIX-based systems, Infinit uses `FUSE` to provide mount points. Hence, for UNIX-based containers, you need `FUSE` installed on your host (see Infinit's [get-started page](https://infinit.sh/get-started#installation)) and run Docker with specific options (`--cap-add SYS_ADMIN --device /dev/fuse`).

	docker run --cap-add SYS_ADMIN --device /dev/fuse -e INFINIT_USER=$USER -v ~/.local/share/infinit:/root/.local/share/infinit --rm infinit volume mount --name <VOLUME> --mountpoint <DIRECTORY>

*NOTE: On Windows systems, Infinit uses `Dokan`, but Windows-native containers aren't officially supported yet by Infinit.*

More file system interfaces will be added in the future to acces file storage logics.

#### Others (object, block, etc.)

At current version (0.8.0), the single logic exposed is the distributed file system but more logics will be added in the upcoming releases, such as an object storage logic, a block device logic and various interfaces for them.

# License

View [license information](https://www.infinit.sh/licenses/infinit.txt) for the software contained in this image.

a container is a runnable instance of an image. you can create, start, stop, move or delete a container using the Docker API or CLI. 

by default a container is relatively well isolated from other containers and its host machine. you can control how isolated a container's network, storage, or other underlying subsystems are from other containers or from the host machine.

any configuration provided to a container when you create or start it will be passed into it. deleting a container means that any changes to its state that aren't stored in persistent storage also disappears.
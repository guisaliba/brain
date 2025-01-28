docker solves the "works on my machine" problem. it enables one developer to ship to a server the exact same environment as they are developing, through an image that lives in a container.

the container, as you can already imagine, contains the image but it cannot live and exist out of nowhere, it has to run inside an OS because it is kind of a process, and as every process, it needs resources such as CPU, RAM etc.

docker has three building steps.
1. build:
2. ship:
3. run:
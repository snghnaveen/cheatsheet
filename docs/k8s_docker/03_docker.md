---
sidebar_position: 3
---

# Docker

### Useful links
| Topic      | 
| ----------- |
| [Docker guide](https://gist.github.com/nicolasdao/f440e76b8fd748d84ad3b9ca7cf5fd12) |



<details>
  <summary> ENTRYPOINT vs CMD </summary>

In Docker, both the `ENTRYPOINT` and `CMD` directives are used to specify the command that will be executed when a container starts. However, they have different behaviors and can be used in different ways:

1. `CMD`:
   - The `CMD` directive is used to provide default arguments for the command that will be executed when the container starts.
   - It is typically used to specify the main command or process that should run inside the container.
   - You can include multiple `CMD` instructions in a Dockerfile, but only the last one will take effect.
   - If the `CMD` instruction is combined with the `ENTRYPOINT` instruction, the `CMD` arguments will be passed as arguments to the `ENTRYPOINT` command.
   - The `CMD` instruction can be overridden by providing a command when running the container using the `docker run` command or by specifying the `CMD` explicitly in the `docker run` command.
   - Example usage:
     ```Dockerfile
     CMD ["python", "app.py"]
     ```

2. `ENTRYPOINT`:
   - The `ENTRYPOINT` directive is used to configure the container as an executable.
   - It specifies the command that will be executed when the container starts.
   - The `ENTRYPOINT` command is not overridden by providing a command when running the container. Instead, any arguments provided at runtime will be passed as arguments to the `ENTRYPOINT` command.
   - If the `ENTRYPOINT` instruction is combined with the `CMD` instruction, the `CMD` arguments will be appended to the `ENTRYPOINT` command.
   - The `ENTRYPOINT` instruction is commonly used to define a container as an executable, with the `CMD` instruction providing default arguments to the `ENTRYPOINT` command.
   - Example usage:
     ```Dockerfile
     ENTRYPOINT ["python", "app.py"]
     ```

To summarize, the `CMD` instruction provides default arguments to the main command, while the `ENTRYPOINT` instruction defines the main command that will run in the container. The `CMD` instruction is typically used for providing defaults and allowing them to be overridden, while the `ENTRYPOINT` instruction is useful when you want to define a container as an executable with fixed behavior.
</details>

---

<details>
  <summary> COPY vs ADD </summary>

In Docker, both the `COPY` and `ADD` instructions are used to copy files and directories from the host machine to the container. However, there are a few differences between the two directives:

1. `COPY`:
   - The `COPY` instruction is used to copy files and directories from the host machine to the container.
   - It supports copying local files and directories, as well as files and directories within the build context (the directory where the Dockerfile resides).
   - The `COPY` instruction only performs a plain copy operation and does not extract compressed files.
   - It is recommended to use `COPY` when you want to copy local files and directories into the container, as it has a simpler and more transparent behavior.
   - Example usage:
     ```Dockerfile
     COPY app.py /app/
     ```

2. `ADD`:
   - The `ADD` instruction has the same functionality as `COPY`, but with some additional features.
   - In addition to copying files and directories, the `ADD` instruction also supports the extraction of compressed files (e.g., .tar, .gzip, .bz2) into the container.
   - If the source file is a compressed archive, `ADD` will automatically extract it to the destination path in the container.
   - The `ADD` instruction can also accept URLs as the source, and Docker will download the file and place it in the container.
   - However, due to the implicit extraction and potential security risks, it is recommended to use `COPY` instead of `ADD` when you are only copying local files and directories.
   - Example usage:
     ```Dockerfile
     ADD app.tar.gz /app/
     ```

To summarize, the `COPY` instruction is preferred for most cases when you want to copy local files and directories into the container. Use the `ADD` instruction if you need the additional functionality of extracting compressed files or want to copy files from URLs. However, be cautious with the implicit extraction and consider the security implications before using `ADD`.
</details>

---


<details>
  <summary> Type of networks in Docker </summary>

In Docker, there are several types of networks available for containers to communicate with each other and with the host machine. Here are some commonly used network types in Docker:

1. Bridge network: By default, when you create a new container, it is connected to the bridge network named "bridge." The bridge network allows containers on the same host to communicate with each other using their IP addresses. Containers connected to the bridge network can also communicate with the external network if port mapping is configured.

2. Host network: When a container is connected to the host network, it shares the network namespace with the host machine, which means it uses the network stack of the host directly. This network mode can provide better performance but may lead to port conflicts if multiple containers use the same ports.

3. Overlay network: Overlay networks enable communication between containers across multiple Docker hosts or Swarm nodes. It is useful for creating distributed applications or services that span multiple machines. Overlay networks use the VXLAN (Virtual Extensible LAN) protocol for encapsulation and provide transparent communication between containers.

4. Macvlan network: Macvlan allows you to assign a MAC address to a container, making it appear as a physical device on the network. This enables containers to have their own IP address on the physical network, allowing them to be directly accessible. Macvlan networks are useful in scenarios where you need to assign IP addresses to containers and have them communicate directly with the physical network.

5. None network: The "none" network mode disables networking for the container. It means the container has no network interfaces or connectivity. This mode can be useful in specific cases where you want to isolate a container completely from network communication.

6. Custom user-defined networks: Docker also allows you to create custom user-defined networks. These networks can be created using the `docker network create` command and provide isolation and connectivity features similar to the bridge network. User-defined networks can be useful for organizing and managing containers within specific network segments.

These are some of the common network types in Docker. You can choose the appropriate network type based on your application requirements and desired communication capabilities between containers.
</details>

---

<details>
  <summary> Difference between a Docker container and a virtual machine </summary>

Docker containers and virtual machines (VMs) are two different technologies used for application deployment and isolation. Here are the key differences between Docker containers and virtual machines:

1. Architecture: Docker containers leverage the host operating system's kernel and share the host's OS resources. They run on a containerization engine (such as Docker Engine) and provide process-level isolation. Virtual machines, on the other hand, emulate an entire operating system environment, including the kernel, and run on a hypervisor. Each VM has its own guest OS, and multiple VMs run on a host system.

2. Resource utilization: Docker containers are lightweight and use fewer system resources because they share the host's OS kernel and libraries. They have faster startup times and lower memory overhead compared to VMs. Virtual machines, on the other hand, require separate resources for each guest OS, including memory, CPU, and disk space, which can lead to higher resource utilization.

3. Isolation: Docker containers provide process-level isolation, which means that each container runs as an isolated process with its own file system, network interface, and namespace. Containers share the host's OS kernel, but they cannot directly access resources outside their container. Virtual machines offer stronger isolation by providing complete OS-level isolation. Each VM runs in its own virtualized hardware environment, including its own kernel, which provides a higher level of isolation between VMs.

4. Portability: Docker containers are highly portable and can be easily moved across different environments. They encapsulate the application and its dependencies into a single unit, allowing for consistent deployment across different hosts and platforms. Virtual machines are also portable, but they typically require a full guest OS, making them slightly less lightweight and flexible compared to Docker containers.

5. Performance: Due to their lightweight nature and shared resources, Docker containers generally offer better performance compared to virtual machines. Containers have lower overhead, faster startup times, and more efficient resource utilization. Virtual machines, on the other hand, have additional overhead from emulating a full hardware environment, which can impact performance.

6. Ecosystem and tooling: Docker has a mature ecosystem and a wide range of tools and services specifically designed for container management and orchestration. There are various container registries, orchestration platforms (such as Kubernetes), and continuous integration/delivery tools that integrate well with Docker containers. Virtual machines have their own set of management and orchestration tools, but the container ecosystem is generally more extensive.

In summary, Docker containers provide lightweight, portable, and efficient application isolation by leveraging the host operating system, while virtual machines offer stronger isolation by emulating an entire hardware environment with dedicated resources for each guest OS. The choice between Docker containers and virtual machines depends on the specific requirements of the application and the desired trade-offs in terms of isolation, resource utilization, and deployment flexibility.
</details>

---

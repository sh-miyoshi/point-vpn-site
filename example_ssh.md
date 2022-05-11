# How to access to SSH server

This page describes how to access the SSH server you manage.

## Before you begin

- SSH server
  - the SSH server that you want to access
- A server to install server agent
  - Anywhere you can access the SSH server (even within the same computer) is ok.
  - Install Docker
  - If you control Outbound communication by Firewall, please allow communication to https://point-vpn-controller.onrender.com and https://router-wq3ixsscka-uc.a.run.app
- Your local PC
  - Install Docker
  - Install SSH Client(ssh command)
  - If you control Outbound communication by Firewall, please allow communication to https://point-vpn-controller.onrender.com and https://router-wq3ixsscka-uc.a.run.app

## Steps

### 1. Login

Access to Point-VPN Console(https://point-vpn-controller.onrender.com) via web browser(chrome, edge, ...)

Select "Sign up" for the first time, or "Login" for the second and subsequent times.

![Login](./images/1_login.png)

If you are logging in for the first time, please also register your User Name after logging in.

![Create User](./images/2_user_create.png)

### 2. Create a project

First, create a Project to manage access.
Note that one Server Agent and multiple Client Agents can be registered in a project.
After logging in, select "New project".
After entering the necessary information, click the "Create" button.
Outgoing Address specifies where the SSH server is accessed from the Server Agent.
Format is `ssh://<username>:<password>@<address>:<port>`.
※SSH currently supports password authentication only; public key authentication is in the works

![Create Project](./images/3_create_project.png)

### 3. Start server agent

Next, start the Server Agent.
From the Project List page, click the "Edit" button for the Project you just created.

![Project Index](./images/4_project_index.png)

Go to the Project Details page, where you can manage Server Agents and Client Agents.
The command to start the Server Agent is displayed by pressing the "Run Command" button in the Server Agent block.
Copy the value and execute it on the server where you want to install the Server Agent.

![Project Show](./images/5_project_show.png)

![Server Agent Run Command](./images/6_run_command.png)

### 4. Register and start client agent

Finally, register and activate the Client Agent.

Click the "Add Agent" button on the Project Details screen of the browser again.

![Project Show](./images/7_project_show.png)

Enter the required information and click the "Create" button.
Specify the address to be accessed by the SSH client in the "Incomming Address" field.
You can enter a user name and password, but they will be ignored for now.

![Create Client Agent](./images/8_create_client_agent.png)

Obtain the startup code from the "Run Command" button as in the case of the Server Agent, and execute it on your PC to start the Client Agent.
After starting the Client Agent, access the address specified in the "Incomming Address" field with the SSH command.

![Client Agent Show](./images/9_client_agent_show.png)

```bash
ssh localhost -p 30000
```

Happy SSH!

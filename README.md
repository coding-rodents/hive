# hive
The main repository for the Hive project. 

## Repo structure

The repository contains 2 git submodules:

1. Hive Backend project reference
2. Hive Frontend project reference

## Cloning

The recommended way of cloning the Hive project is through cloning this repository with the submodules. This way, a proper directory tree is created and devcontainer features can be used for launching the backend and frontend in a configuration that connects their containers.

Cloning through GitHub Desktop clones the submodules automatically and is the most effortless way in my opinion. For guide in cloning through git CLI, see git docs.

## Devcontainers

The project contains `.devcontainer/` directory that has separate devcontainers configuration for launching the backend project and frontend project. 

### Specs

- Docker is needed
- Recommended IDE is **Visual Studio Code with** `Dev Containers` **extension installed**

### Configuration (first launch)

1. Open the main repository folder in Visual Studio Code.
2. Create a `.env` file inside `docker/` directory, based on `docker/.env.template`
3. Open the command pallete in VSCode (ctrl + shift + P), search for `Dev Containers: Reopen in Container`, select it and choose `Hive Backend`.
4. VSCode will build and launch the `backend` and `db` container services from the compose file. After that, the Java environment will be initialized (this takes a while). After that the backend dev container is ready.
5. Open another VSCode window and open the main repository folder inside it again.
6. Open the command pallete, search for `Dev Containers: Reopen in Container`, select it and choose `Hive Frontend`.
7. VSCode will build and launch the `frontend` container service from the compose file. After that, npm will run and install Angular CLI. After that is finished, open a new terminal, make sure you are in the frontend project directory with `package.json` file in it. Run `npm install` in the terminal - this will install all package dependencies.

### Launch

#### Backend

TBD

#### Frontend

Open a terminal in the frontend project directory with `package.json` in it and run the `npm run devc-start` command. This runs `ng serve` with necessary arguments that make the angular dev server visible to the host machine.

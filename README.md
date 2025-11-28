<div align="center">
  <img alt="Hive logo" 
    src="https://github.com/user-attachments/assets/8b219a51-6b11-495a-92dc-0c59a5e21f75" 
    width=300 />
</div>

# Hive

Hive is a concept platform for organising and maintaining timetables, discussions, as well as a useful tool for being up-to-date, dedicated to university students.
It was created as a project for a course at Silesian University of Technology, with potential plans for polishing and future development.
Why the name Hive? Well, let's be honest - students at universities can be very busy and daily life can seem like in a busy beehive.

## Description

The main principle of the platform is to allow students to maintain their own versions of timetables and a uniform information feed, that can be managed by them.
During a term - hours when some classes take place can shift and sometimes, some of this may not be reflected in official timetables - this is when unnecessary complications begin.

With the platform, students can create groups, timetables and posts, update them according to what is happening and create other events, that are outside the scope of a traditional timetable, such as time blocks that remind people about an upcoming exam etc.
A major advantage of the system is the ability to filter out content that an example user might not want to receive information and updates about through a mechanism of tag subscription.
Users can tailor their dashboard and notifications to their needs and be up to date with information that they care about the most.

## System structure

### Backend

The backend is written in Java, using the Spring framework in a service-oriented architecture.
For data storage, we used containerized PostgreSQL database.
Security is maintained through use of Spring Security and integration of JSON Web Tokens.

### Frontend

The frontend is written in TypeScript, with use of Angular and plain CSS for styling.
Authentication and authorization is well maintained and the website behaves according to given user's privileges.

## Development

### Repo structure

The repository contains 2 Git submodules:

1. Hive Backend project reference
2. Hive Frontend project reference

### Cloning

The recommended way of cloning the Hive project is through cloning this repository with the submodules.
This way, a proper directory tree is created and devcontainer features can be used for launching the backend and frontend in a configuration that connects their containers.

Cloning through GitHub Desktop clones the submodules automatically and is the most effortless way.
For guide in cloning through git CLI, see git docs.

After cloning the repository with the submodules, go into both backend and frontend repositories and checkout to the named versions of the branches (submodules are tracked by commit hashes, so to keep things clean, switch the submodule repository branch to the named version to avoid confusion).

### Local development

#### Dependencies

`Docker` is required for managing the containerized database.

Both backend and frontend repositories have their own README files, where versions of required dependencies are listed. The dependencies are:

- Backend: `JDK 21`
- Frontend: `NodeJS v20 LTS`, `Angular CLI ~18.2.9`

#### Configuration and launch

Create a `.env` file inside `docker/` directory, based on `docker/.env.template`.

##### Backend

Open the `backend/hive/` project directory in preferred IDE (VSCode / IntelliJ are fine).
The project should load normally and Gradle will take care of fetching the dependencies and building the app.
The spring profile configuration in `application.yml` should be set to `"devlocal"`. 

To launch the backend app, the database also needs to be running.
To manage the database service container with Docker Compose, here are useful commands (to execute the compose commands successfully, you must be in the `docker/` directory with `docker-compose.yml` in it):

###### Launch the database container
```sh
docker compose up -d db
```

###### Stop and remove the database container
```sh
docker compose down db
```

###### Check the status of running containers
```sh
docker ps
```
Or just look at the Docker Desktop dashboard on Windows / macOS.

##### Frontend

Open the `frontend/` directory in the preferred IDE (VSCode is fine).
In this directory with `package.json` in it, execute `npm install` in the terminal - this will fetch the required dependencies.
To run the app, execute `ng serve` in the terminal.

### Containerized development (Devcontainers)

The project contains `.devcontainer/` directory that has separate devcontainers configuration for launching the backend project and frontend project. 

#### Dependencies

- Docker is needed
- Recommended IDE is **Visual Studio Code with** `Dev Containers` **extension installed**

#### Configuration (first launch)

1. Open the main repository folder in Visual Studio Code.
2. Create a `.env` file inside `docker/` directory, based on `docker/.env.template`
3. Open the command pallete in VSCode (ctrl + shift + P), search for `Dev Containers: Reopen in Container`, select it and choose `Hive Backend`.
4. VSCode will build and launch the `backend` and `db` container services from the compose file. After that, the Java environment will be initialized (this takes a while). After that the backend dev container is ready.
5. Open another VSCode window and open the main repository folder inside it again.
6. Open the command pallete, search for `Dev Containers: Reopen in Container`, select it and choose `Hive Frontend`.
7. VSCode will build and launch the `frontend` container service from the compose file. After that, npm will run and install Angular CLI. After that is finished, open a new terminal, make sure you are in the frontend project directory with `package.json` file in it. Run `npm install` in the terminal - this will install all package dependencies.

#### Launch

##### Backend

TBD

#### Frontend

Open a terminal in the frontend project directory with `package.json` in it and run the `npm run devc-start` command. This runs `ng serve` with necessary arguments that make the angular dev server visible to the host machine.

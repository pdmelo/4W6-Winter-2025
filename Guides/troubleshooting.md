# Troubleshooting

## 1. psql connection error 'error: connection to server at "localhost" (::1), port 5432 failed'

![psql-connection-error](../images/troubleShooting-psql.png)

Option 1. Close remote Connection, then reopen folder in Container.

Option 2. Restart docker.

Option 3. If that doesn't fix it
1. Close connection to the remote container
2. delete the container and its associated volume in the docker
3. Reopen the folder in the container..



## 2.  code: 'ERR_MODULE_NOT_FOUND',
![troubleShooting-ass1-module-not-found.png](../images/troubleShooting-ass1-module-not-found.png)

Check the path to your Todo.ts file, run the ts file from its location.
![ts-moduleNotFound-Solution](../images/ts-moduleNotFound-Solution.png)

## 3. Cannot stop Docker Compose application. Reason: compose [stop] exit status 125.
Navigate to the directory where your docker-compose.yml file is located in, i.e .devcontainer . Do this only if your Docker appears to hung and you not able to stop a container via the docker desktop application.
**`docker-compose stop`** only **stops** the containers but does **not remove** them.



## 4.Dev Container configuration ‘.devcontainer/devcontainer.json’ file already exists

1. Go to your VS Code extensions (icon of the four squares on the left sidebar).
2. Click on “Dev Containers”.
3. Click on “Switch to Pre-Release”.
4. Click on “Reload”.

## 5.Typescript Error
```Bash
Cannot find type definition file for 'express'.
  The file is in the program because:
    Entry point of type library 'express' specified in compilerOptionsts
Cannot find type definition file for 'node'.
  The file is in the program because:
    Entry point of type library 'node' specified in compilerOptionsts
```

**Solution:**

Opening any TS file > CMD + SHIFT + P >  on mac OR CRTL + SHIFT + P on windows 

```bash
TypeScript: Restart TS Server
```




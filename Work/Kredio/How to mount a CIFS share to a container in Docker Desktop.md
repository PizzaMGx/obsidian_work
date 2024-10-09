I use this solution because mounting the CIFS from docker desktop does not work

```
# Error mounting volume, WSL issue I believe
  mount-vol:
    driver: local
    driver_opts:
      type: nfs
      o: "addr=192.168.1.25"
      device: ":/Media"
```

First problem, Docker Desktop uses an alpine based WSL2 image, and this image is missing the cifs-utils package.. this needs to be installed
Open the Windows command prompt

```
wsl --distribution docker-desktop
apk add cifs-utils
```

Now switch back to Docker Desktop, and using the Portainer Extension, you can define a volume that maps to the CIFS share as follows:

![[Pasted image 20241004110417.png]]

Note: substitute the IP address of your CIFS target (dont use dns name as that just adds complexity), and add in a username and password that has access to the CIFS share.

Now you can add this volume to a container..

```
container:
    volumes:
      - mount-vol:/Mount

volumes:
  mount-vol
```

Enjoy
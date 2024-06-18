# Run dockers without root/sudo

- Create the docker group if it does not exist
```
sudo groupadd docker
```
- Add your user to the docker group.
```
sudo usermod -aG docker $USER
```
- Log in to the new docker group (to avoid having to log out / log in again; but if not enough, try to reboot):
```
newgrp docker
```
- Check if docker can be run without root
```
docker run hello-world
```
- Reboot if still got error
```
reboot
```
## Refernce
- https://stackoverflow.com/questions/48957195/how-to-fix-docker-got-permission-denied-issue

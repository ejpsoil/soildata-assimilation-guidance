---
title: Overview Local Tunnel
summary: 
authors:
    - Paul van Genuchten
date: 2023-01-05
---

# Overview Local Tunnel

This recipe describes an approach to temporarily host a local webservice as an online service. A utility opens a tunnel to a service provicer, the service provider routes all traffic for a specific domain via the tunnel to your machine. The tunnel stops if you quit the utility (ctrl-c).

Various (free) service providers exist offering this service:

- [localtunnel](https://theboroer.github.io/localtunnel-www/) requires nodejs 
- [ngrok](https://ngrok.com) web based, but requires registration 
- [localhost.run](https://localhost.run) requires SSH to be installed

## Exercise

- Verify a docker image is running, for example: 

  ```
  docker run -p 80:80 -d uzyexe/tetris:latest
  ```

- Enter this command:
  
  ```
  ssh -R 80:localhost:80 nokey@localhost.run
  ```

- The utility will display a url on which the service will be available, try this url in your browser (and phone, to make sure it works also outside your computer)

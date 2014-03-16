microwave
=========



- Orchestrates the deployment of virtual machine images (built with Packer), and linux container images (built with Docker)
	- http://www.packer.io
	- https://www.docker.io
- Repeatable deployments because your images will always be deployed the same way
- Persistent volumes for databases and other storage that must survive a re-deployment
- Fast! 
	- Micro upgrades to your deployment - changes to single containers deployed quickly
	- Add more identical hosts to scale quickly - they are just images



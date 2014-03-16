How to orchestrate a Docker + Packer image deployment

Assumptions
===========
- Lets go with Amazon Web Services 
- We have a manifest file describing a single environment
	- VPCs, VPNs, Security Groups
		- The creation of these may be out of scope.
	- Hosts 
		- name
		- image id (building images out of scope)
		- VPCs, VPNs, Security groups
		- persistent volume information
		- Docker container information
		- delta provisioners - puppet, ansible, shell, etc.
	- Containers 
		- name
		- image id (building images is out of scope - all we need is image on a registry)
		- port mappings
		- volumes
		- any other items that go on the docker run command line


Algo 1: Always clean Big Bang - simple - slow upgrades
======================================================
- Terminate all VMs, taking care not to delete persistent volumes
- Create any missing persistent volumes (as compared to the manifest)
- Don’t delete any obsoleted persistent volumes 
	- Just warn about them - never lose user data
- Create all hosts with persistent volumes attached
- Run all delta provisioners
- Run all required containers on all hosts

Faster
=====
- work out which hosts have wrong images 
	- rebuild from scratch as with Algo 1.
	- attaching and detaching storage
	- or even build stand in place host first and move storage 
- if host images are right, but docker images are wrong
	- Stop container
	- Start with new image, and new options
- Done?
	- What about the delta provisioners?
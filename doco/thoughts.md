How to orchestrate a Docker + Packer image deployment

Assumptions
===========
- We have a manifest file describing a single environment
- Lets go with Amazon Web Services


Technique 1: Always clean Big Bang
============================
Terminate all hosts, taking care not to delete persistent volumes
Create any missing persistent volumes
Don’t delete any obsoleted persistent volumes - just warn about them
Create all hosts with persistent volumes attached
Run all required containers on all hosts

Faster
=====
- work out which hosts have wrong images 
  - rebuild from scratch 
  - attaching and detaching storage
  - or even build stand in place host first and move storage 
- if host images are right, but docker images are wrong
  - for containers that need storage
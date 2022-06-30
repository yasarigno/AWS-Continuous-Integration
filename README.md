# AWS-Continuous-Integration
I built an AWS Cloud9 development environment and integrate it with GitHub Actions. The project contains a simple algorithm written in Python. I plan to change it with a more useful one.

## Steps to follow :

1. Create the files on Cloud9
2. Delegate GitHub to clone the files from AWS. To do this we need to create an SSH key on Cloud9.

ssh-keygen -t rsa 

cat /home/ec2-user/.ssh/id_rsa.pub



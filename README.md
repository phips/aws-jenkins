# Spin up Jenkins on AWS EC2 using Ansible

## Introduction

This is an [Ansible](http://ansibleworks.com) playbook to install and run the
[Jenkins CI](http://jenkins-ci.org/) system on an 
[AWS EC2](http://aws.amazon.com/ec2) instance.

Jenkins is started as its own service, and not proxied via a web server. That
is left as an exercise for the reader :-)

## Running

Naturally, you need [Ansible](http://ansibleworks.com) installed on your
host system before using this.

You will also need to export AWS_ACCESS_KEY and AWS_SECRET_KEY as environment
varibles before running the playbook. These are your AWS access values.

Then run ``ansible-playbook ec2.yaml -e 'keypair=FOO'`` where FOO is the name of your [AWS keypair](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html).

## Details

Note this play is written to ONLY run on an RPM based distro. You could always
extend/alter it to work on a dpkg based distro. Additionally, it also makes
some assumptions based on the AMI used - the Amazon Linux AMI already has a
usable Java installed, so we don't need to handle that here.

The first part of the play, the ec2.yaml file, will spin up a single, 
[t1.micro](http://aws.amazon.com/ec2/instance-types/#instance-details),
[Amazon Linux](http://aws.amazon.com/amazon-linux-ami/) instance in eu-west-1.
Variables to control these elements are defined at the top of the playbook, in
the vars section. You can change these as required, either in the file or on
the command line with --extra-vars passed to ansible-playbook.

If you have DNS in [Route53](http://aws.amazon.com/route53/) the play can also
create a DNS entry. By default this is not set to run, but specify
``--extra-vars="set_dns=True dns_zone=ZONENAME"`` at runtime and an entry
``ci.ZONENAME`` will also be created.

*NOTE*: The first part of the play, 'ec2.yaml' will create a new EC2 instance
**every time it is run**. This is the nature of the ec2 module.



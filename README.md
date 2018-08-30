# packer-templates

### quickstart

To run

```
packer build -var-file=variables/your_var_file.json ubuntu_base.json
```

### variables
There's a variables template in the respective folder. I have a git ignore on further json files there. Don't be the person who commits secrets to public repos.

I don't include the expected variables in the packer templates in order to enforce that you include everything that's required.

### requirements

Install packer. On a mac you can easily do this with:

```
brew install packer
```

See here for other install info: https://www.packer.io/docs/install/index.html

If you want to use a provider that's local to the cloud system, make sure you install it with the shell script provider. There's a scripts folder to store those kinds of scripts.

Here's an example of the shell script provider for an ubuntu box, with root privs

```
{
    "type": "shell",
    "execute_command": "echo 'ubuntu' | sudo -S -E bash {{.Path}}",
    "scripts": [
      "scripts/your_script.sh",
      "scripts/your_second_script.sh"
    ]
}
```

If you want to use something that connects to the instance from your machine for provisioning (like ansible), make sure it's installed on your local machine.

### finding ami-id owners

```
aws ec2 describe-images --image-ids <an AMI id>
```

It will have output you can discern the owner ID from.

### bits and pieces

I have a variable where you can define a security group. Do this if you have a prebuilt packer SG that knows all the source IPs you might connect from. If you have a VPN where the egress IP address could change, or your IP changes often, that could be annoying to track; I have it excluded from the template for that reason. You'll need to reference the packer docs for the right KV to add to your template.

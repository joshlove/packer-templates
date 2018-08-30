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

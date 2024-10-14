# Initial Setup

## First you need to set up your identity

First set up your Git identity. This is the identity your Git commit will use.

If you don't want to expose your email, it is recommended to [use your no-reply email in GitHub](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address?platform=windows). For most companies, you will use your work email address.

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

Recommend you also set this alias for seeing the Git commit history.

```bash
git config --global alias.tree "log --graph --decorate --pretty=oneline --abbrev-commit"
```

It is recommended to also set this, as this will automatically set the upstream branch when you push a branch:

```bash
git config --global push.autoSetupRemote true
```

## HTTPs or SSH

This is the technology used to talk to Git repository. Most companies will dictate the technology used.

If you have to choose, I would recommend HTTPs. This is because most Git providers (GitHub, Azure DevOps, GitLab) support OAuth which makes it much easier to use.

## Certificate issues

Using HTTPs causes some pains with certificates. If you company uses a Proxy, HTTPs interceptor or several other security tools the certificate you see on request may not be the one Git expects. Before you do the below check with your security team that this is actually what is happening, or this could actually be a "man-in-the-middle" attack and you are allowing someone to steal all your secrets.

**If security confirms you use the above, then follow the below.**

You will need to allow this certificate for it to work. **DO NOT RUN THE BELOW COMMAND, this ia bad thing to do.**

```bash
# DO NOT RUN THIS COMMAND
# git config --global http.sslVerify false
```

Instead get the certificate in the middle by running the below commands.

```bash
echo | openssl s_client -showcerts  -connect <host>:<port> -servername <host> 2>/dev/null </dev/null |  sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p'

# Example for GitHub
echo | openssl s_client -showcerts  -connect dev.azure.com:443 -servername dev.azure.com 2>/dev/null </dev/null |  sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p'

# Example for Azure DevOps
echo | openssl s_client -showcerts  -connect dev.azure.com:443 -servername dev.azure.com 2>/dev/null </dev/null |  sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p'
```

You need to grab the last certificate in the chain, as this is the Certificate Authority (CA) certificate. There may only be one if you are using a proxy. You want to grab the bottom `-----BEGIN CERTIFICATE----- ... -----END CERTIFICATE-----`. Copy the contents. You will need to add this to the CA trust store Git uses.

```pem
-----BEGIN CERTIFICATE-----
MIII6zCCBtOgAwIBAgITMwCCiBmpqSLTCn0wfgAAAIKIGTANBgkqhkiG9w0BAQwF
...
MG4YiELqgCAWaik2eBJT2j0EWGEif4qnJxQ+/8GK3w==
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
MIIFrDCCBJSgAwIBAgIQCkOpUJsBNS+JlXnscgi6UDANBgkqhkiG9w0BAQwFADBh
...
2u7wY2uLYpgK0o3X0iIJmwpt7Ovp6Bs4tIE/peia+Qcdk9Qsr+1VgCGA==
-----END CERTIFICATE-----
```

You have 2 options then:

- If you are able you can add this to the Git install. Add this file to the bottom of the Git install path: `C:\Program Files\Git\usr\ssl\certs\ca-bundle.crt`.

- If you cannot, copy the contents of `C:\Program Files\Git\usr\ssl\certs\ca-bundle.crt` to `C:\Git\ca-bundle.crt` (you can put this anywhere). Then add the CA certificate you copied to the bottom of the file. Then run this command which will tell Git to use the new `ca-bundle.crt` for that specific host.

```bash
# Required if you create a new ca-bundle.crt
git config --global http."https://<host>/".sslCAInfo C:\Git\ca-bundle.crt
```

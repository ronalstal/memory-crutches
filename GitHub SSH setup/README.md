
## Setting up GitHub ssh

### 2017-11-04

#### Get SSH keys

```
ssh-keygen -t rsa -b 4096 -C "ronalstal@gmail.com"
# run ssh agent server in background and add the key
# (no passphrase used)
eval "$(ssh-agent -s)"
ssh-add id_rsa
# copy the public key to the clipboard
xclip -sel clip < ~/.ssh/id_rsa.pub
```

#### insert the keys in [GitHub Account Keys Settings](https://github.com/settings/keys)

#### configure git

```
# testing the SSH connection
ssh -T git@github.com
# -> Hi ronalstal! You've successfully authenticated, but GitHub does not provide shell access
```

Edit `~/.ssh/config`:

```
Host github.com
  User git
  Hostname github.com
  IdentityFile ~/.ssh/id_rsa
```
where the IdentityFile is the private key file created above.

In your projects, change the FETCH and PUSH urls:
```
$ git remote show origin
>> * remote origin
>>  Fetch URL: https://github.com/ronalstal/memory-crutches.git
>>  Push  URL: https://github.com/ronalstal/memory-crutches.git
>>  HEAD branch: (unknown)
>>  Local branch configured for 'git pull':
>>    master merges with remote master

# change https to ssh in the git config editor:
$ git config -e

$ cat .git/config
>> [core]
>> 	repositoryformatversion = 0
>> 	filemode = true
>> 	bare = false
>> 	logallrefupdates = true
>> [remote "origin"]
>> 	url = ssh://github.com/ronalstal/memory-crutches.git
>> 	fetch = +refs/heads/*:refs/remotes/origin/*
>> [branch "master"]
>> 	remote = origin
>> 	merge = refs/heads/master

$ git remote show origin
>> * remote origin
>>   Fetch URL: ssh://github.com/ronalstal/memory-crutches.git
>>   Push  URL: ssh://github.com/ronalstal/memory-crutches.git
>>   HEAD branch: (unknown)
>>   Local branch configured for 'git pull':
>>     master merges with remote master

```

#### documentation

. [Connecting to GitHub with SSH (GitHub Help)](https://help.github.com/articles/connecting-to-github-with-ssh/)  
. [Superuser: How to tell git which private key to use?](https://superuser.com/questions/232373/how-to-tell-git-which-private-key-to-use)

## LICENSE

MIT, Copyright (c) 2017 Ronald Stalder @ronalstal.gmail.com  
See [LICENSE.txt](LICENSE.txt)

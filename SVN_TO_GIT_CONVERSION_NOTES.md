## NOTES ABOUT SVN to GIT CONVERSION

Set up working dir:

```
cd /usr/local/
mkdir ceda-cc
cd ceda-cc/
```

Check the authors and set authors file:

```
svn log --quiet http://proj.badc.rl.ac.uk/svn/exarch/CCCC | grep -E "r[0-9]+ \| .+ \|" | cut -d'|' -f2 | sed 's/ //g' | sort | uniq
```

This showed most authors had moved on so no need to maintain. Just maintain Martin and Ag in authors file: `authors.txt`

Installed dependencies for script, and then script itself:

```
yum install -y git svn git-svn ruby rubygems
gem install svn2git
```

Run script itself (specifying author map):

```
svn2git http://proj.badc.rl.ac.uk/svn/exarch/CCCC --authors authors.txt
```

Updated remote settings in git config file: `.git/config`:

```
[remote "origin"]
	fetch = +refs/heads/*:refs/remotes/origin/*
	url = https://agstephens@github.com/cp4cds/ceda-cc
[branch "master"]
	remote = origin
	merge = refs/heads/master
```

Update `setup.py` to point to new GitHub location:

 https://github.com/cp4cds/ceda-cc

Push to master:

```
git push -u origin master
git push
git push origin --all  # to push branches
git push origin --tags # to push tags
```


# Gentoo-overlay : A custom ebuild repository for gentoo

Because some .ebuild files on the official Gentoo repository are not compatible with Gentoo Prefix.

## Defining a custom ebuild repository

```sh
mkdir -p $EPREFIX/var/db/repos/localrepo/{metadata,profiles}
echo 'localrepo' > $EPREFIX/var/db/repos/localrepo/profiles/repo_name
cat << "EOF" > $EPREFIX/var/db/repos/localrepo/metadata/layout.conf
masters = gentoo
auto-sync = false
EOF
```


## Add repository to portage

```sh
cat << EOF > $EPREFIX/etc/portage/repos.conf/localrepo.conf
[localrepo]
location = $EPREFIX/var/db/repos/localrepo
EOF
```

```sh
[localrepo]
location = $EPREFIX/var/db/repos/localrepo
```

## Adding an ebuild to the repository

```sh
mkdir -p $EPREFIX/var/db/repos/localrepo/app-dicts/artha
vim $EPREFIX/var/db/repos/localrepo/app-dicts/artha/artha-1.0.2.ebuild
#chown -R portage:portage /var/db/repos/localrepo  # do not chown on Gentoo Prefix
pushd $EPREFIX/var/db/repos/localrepo/app-dicts/artha/artha-1.0.2.ebuild
repoman manifest
popd
```

# lrepo
Expansion Android Repo, you can
- check some project infomation
- use current commit id compare with remote commit id
- use current commit id compare with revision(manifast.xml) commit id
- auto create and push project to gitlab
- export project to file by some filter

# Dependence

[Repo](https://code.google.com/p/git-repo/)  
[GitPython](https://gitpython.readthedocs.io/en/stable/intro.html)   
[Python-Gitlab](https://python-gitlab.readthedocs.io/en/stable/install.html)  
You can use it after `repo init` & `repo sync`.

# Use It
check some project
```bash
$ lrepo device/common/
```
```
device/common
project.name            = device/common
project.remote          = aosp
project.revisionId      = d49a18a17d624b41bcf79ad972ebfdb93f4c2045
project.upstream        = refs/tags/android-7.1.2_r6
git.active_branch  = rockpi-n-all
git.commit         = d49a18a17d624b41bcf79ad972ebfdb93f4c2045
git.remote         = daa24b7bcb65f77a278e94690a9e9862abb6a288
```
compare with remote commit id, if not equal it will print infomation
```bash
$ lrepo remote
```
```
project:external/lzma
// not equal
remote.name     = aosp
remote.upstream = refs/tags/android-7.1.2_r6
remoteId        = a89adaf2e2c16a6cd8df4d91b2237b53e4889af6
commitId        = 26b927f9aae35767f9fff824765d48ea98a282a7
project:bootable/recovery
// equal
Set project upstream to:rockpi-n-all
project:hardware/google/apf
remote.name     = aosp
remote.upstream = refs/tags/android-7.1.2_r6
remoteId        = 378c360c9195d2becbf00f9d6bfae1161c56aa02
commitId        = f80b9d17d393b75fbb41971a9ecc30b098a00d55
project:external/icu
remote.name     = aosp
remote.upstream = refs/tags/android-7.1.2_r6
remoteId        = 88cb353a924f948a6d9467cdb4afcfd146134960
commitId        = 18c86be3562ecbfaffd4a42b4fcc702874acf605
project:external/mpp-demo
// equal
```
compare with revision(manifast.xml) commit id
```bash
$ lrepo rev
```
```
// equal
project:external/lzma
project:bootable/recovery
Set project upstream to:rockpi-n-all
project:hardware/google/apf
project:external/icu
project:external/mpp-demo
project:prebuilts/gcc/linux-x86/x86/x86_64-linux-android-4.9
project:system/update_engine
project:external/google-fonts/dancing-script
project:external/io
project:packages/apps/RetailDemo
project:hardware/rockchip/librga
project:external/apache-harmony
project:external/iw
project:system/core
Set project upstream to:rockpi-n-all
```
auto create and push project to gitlab
```bash
$ lrepo gitlab -h
```
```
Usage: gitlab [-t|--token] [-g|--group] [-v|--visibility] PATH

Options:
  -h, --help            show this help message and exit
  -u URL, --url=URL     what url do you want to upload
  -g GROUP, --group=GROUP
                        gitlab group id or name
  -t PRIVATE_TOKEN, --token=PRIVATE_TOKEN
                        gitlab private_token
  -r REMOTE, --remote=REMOTE
                        manifest which remote to gitlab
  -v VISIBILITY, --visibility=VISIBILITY
                        gitlab create visibility
```
export project to file by some filter
```bash
$ lrepo export -h
```
```
Usage: export [-b|--by] <attr> [-g|--grep] <filter> [-o|--out] <PATH>

Options:
  -h, --help            show this help message and exit
  -b ATTR, --by=ATTR    what attr export for example: remote
  -g GREP, --grep=GREP  what to grep with filter result
  -e, --equal           equal <grep> with filter result
  -s, --opposite        opposite result with filter to result
  -o OUT, --out=OUT     out file

```
for example
org_manifast.xml
```
<project groups="pdk-cw-fs,pdk-fs" name="platform/external/strace" path="external/strace" revision="372fd474dea063e08f8faf9abdf0a2bad06a7955" upstream="refs/tags/android-7.1.2_r6"/>
......
<project name="rk/rkbin" path="rkbin" remote="vamrs-vendor" revision="21756f5b5a108fb9d4fd1ffcdb819474892d937f" />
.......
```
```bash
$ lrepo export -b upstream -g refs/tags/android-7.1.2_r6 -e
# out put
# <project groups="pdk-cw-fs,pdk-fs" name="platform/external/strace" path="external/strace" revision="372fd474dea063e08f8faf9abdf0a2bad06a7955" upstream="refs/tags/android-7.1.2_r6"/>
$ lrepo export -b upstream -g refs/tags/android-7.1.2_r6 -e -s
# out put
# <project name="rk/rkbin" path="rkbin" remote="vamrs-vendor" revision="21756f5b5a108fb9d4fd1ffcdb819474892d937f" />
```
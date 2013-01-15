synchronizis
============

This is a Git hook to synchronize with other repositories on pushes. It mirrors
a Git repository to one or more target repositories.

This is a post-update Git hook (if you do not know what a Git hook is, see
"git help hooks") and does the mirroring on every push to the repository.

It must be copied to <git repository>/hooks/post-update (and made executable)
to be used. Additionally, some Git config variables must be set on the
repository:

  mirroring.enabled = (true | false)

    Whether to enable or disable automatic mirroring

  mirroring.targets = target1 [target2 ...]

    Target (mirror) repositories to be used. This is a space separated list
    of Git repository URLS, like the ones used in "git push". See the section
    "GIT URLS" in "git help push" for more infomartion.

    Any of the Git supported URLS will work, as long as no user interaction
    is needed (i.e. no password prompts). The most common cases are local
    repositories and remote repositories over SSH using key authentication.

    For example, to mirror to the remote repository "mirror.git" located at
    server "hostname" over SSH and to the local repository "local-mirror.git":

      "git@hostname:/remote/mirror.git /home/joe/local-mirror.git"

  mirroring.sources = [source1 [source2 ...]]

    This is optional. If not set or set empty, the whole Git repository will
    be mirrored (i.e. any branches or tags). If set, only the specified refs
    (branches or tags) will be mirrored.

    This is a space separated list of gitolite-like refexes (ordinary Git refs
    specified as regular expressions). For more information, see:
    http://sitaramc.github.com/gitolite/refex.html. Examples below.

    Sets only branches whose names start with "stable/" and tags whose
    names start with "release-" to be mirrored:

      "refs/heads/stable/ refs/tags/release-"

    The prefix "refs/heads/" can be omitted if prefered:

      "stable/ refs/tags/beta-release-"

    Sets only the branch "master" and the tag "release-1.0" to be mirrored:

      "master$ refs/tags/release-1.0$"

    Note the character "$". It is required to specify single branches or tags
    instead of "all branches (or tags) whose names that start with ...".

    IMPORTANT: for compatibility with gitolite, the character "!" may be used
    instead of the character "$", with same effect as explained above.


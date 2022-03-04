---
id: v08egsqxbv3m0u532jzo03l
title: Specify alternate project-level README on Github
desc: ''
updated: 1646400894358
created: 1646400876711
---
[Stackoverflow source](https://stackoverflow.com/a/49981731/5930856)
<br>
<br>

[Github Searches for README.md in a few places](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes)

>If you put your README file in your repository's root, docs, or hidden .github directory, GitHub will recognize and automatically surface your README to repository visitors.

To use another file as the project level readme create a [Symlink](https://en.wikipedia.org/wiki/Symbolic_link) from the file to a location inside ```.github``` folder **in the project root**.

### On Linux and Mac
  ```Shell
  # From repository root
  mkdir .github
  cd .github
  ln -s ../docs/projectname/some-README.md README.md  
  ```
### On Windows

Symbolic links are only available on NTFS filesystems on Windows Vista or later, and creating them requires [Developer Mode](https://blogs.windows.com/windowsdeveloper/2016/12/02/symlinks-windows-10/). They are not supported by [Git on Windows out of the box](https://github.com/git-for-windows/git/wiki/Symbolic-Links).

1. `cd` to the root of the repo and enable symlinks:
  ```Shell
    git config core.symlinks true
  ```
2. Launch `cmd.exe` as Administrator:
  ```Shell
  # From repository root
  mkdir .github
  cd .github
  mklink README.md ..\docs\projectname\some-README.md
  ```
3. Ensure there are no other README files anywhere else that github searches in.
4. Windows users who clone the repository won't get a symlink automatically. If they wish to have that behaviour they should clone with a special argument:
   ```Shell
   git clone -c core.symlinks=true <repo-url>
   ```


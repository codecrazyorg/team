# CODECRAZY

## PURPOSE

We write `computer code` to build crazy cool things.

## WEBSITE

Our website is [CodeCrazy.org](https://codecrazy.com): <https://codecrazy.org>

## GITHUB PROJECT REPOSITORY

Please view our current projects by visiting [our GitHub organization page](https://github.com/codecrazyorg) at [https://github.com/codecrazyorg](https://github.com/codecrazyorg).

## VSCODE ONLINE CODESPACE (TEAM ONLY)

If you are a `Code Crazy` team member, [click here](https://ogmath-codecrazyorg-team-r474q5grpf5r96.github.dev/) to access our **[Team Codespace](https://ogmath-codecrazyorg-team-r474q5grpf5r96.github.dev/)** to run **VS Code** from your web browser.

## CLONE OUR TEAM REPO

To clone our main `team` repo `install Git`[^1] then run one of the following commands:

### **HTTPS**

   If using **Unix**, **Linux**, or **BSD**[^3]:

   ```
   sudo git clone https://github.com/codecrazyorg/team.git
   ```

   If using **Windows Powershell**[^4] or **MacOS Terminal**[^bignote]:

   ```
   git clone https://github.com/codecrazyorg/team.git
   ```

### **SSH**[^6]

   ```
   git@github.com:codecrazyorg/team.git
   ```

### **GITHUB CLI**

   ```
   gh repo clone codecrazyorg/team
   ```

## COMMIT AND PUSH CHANGES TO REPO

1. LEARN HOW TO USE GIT

[This link](https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html) will show you the basic steps of using Git's version control commands to initialize your local directory, clone repos, make changes and commit those changes, push and pull, etc., basically everything: <https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html>

2. OBTAIN A PERSONAL SECURITY TOKEN

Team members are now required to obtain a [personal security token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) in place of the old password system. [Click here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) to learn how to get your personal security token. Once you get your token, store it in a safe place because it's never going to be shown to you again. You will enter the token ID in the password field when prompted after doing a `git push origin main`[^2] command.

3. CLONE THE REPO AND ADD OR CHANGE SOMETHING

## LICENSE

Our projects all fall under the [MIT License](https://opensource.org/licenses/MIT); we are supporters of the [Open Source Software Initiative](https://opensource.org/).

## CONTACT

[Email us](mailto:team@codecrazy.org):

```
team@codecrazy.org
```

[^1]: You may install Git either using a [command-line only tool](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), Git's own [standalone GUI](https://git-scm.com/downloads), a [third-party GUI client](https://git-scm.com/downloads/guis), or [run Git *inside* VSCode](https://code.visualstudio.com/docs/editor/versioncontrol).

[^2]: Until *very* recently, the default push to branch was called `master`. GitHub changed the default branch to `main` a few months ago. The issue is that quite a few (if not most) online Git-related tutorials will *insist* you push commits by typing the command `sudo git push origin master` when, in reality, there is no `master` branch in repositories created after the `main` change went into effect. Just keep that in mind: the correct command for newer repositories (including this one) is (if using Linux/BSD/Mac) `sudo git push origin main`.

[^3]: If using **OpenBSD** you *may* need to replace `sudo` with `doas` depending on your implementation.

[^4]: For Windows users you may need to **run as administrator**

[^bignote]: To install Git using the MacOS command line interface, open the Terminal app by using hotkey shortcut `Shift - Command(⌘) - U` then paste this command:

      ```
      git --version
      ```

[^6]: The SSH clone method is only for `code crazy` team members

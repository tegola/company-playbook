

## Prerequisites and definitions

* `develop` is the *integration branch*
* *Gitlab* is the issue tracker
* We are using *Gitlab* or *GitHub* as git server
* `REPO` is our project repository on git server (eg. `git@gitlab.sparkfabrik.com:sparkfabrik/websites/sparkfabrik-tech-blog.git`)

## Steps

Follow these steps to achieve code serenity:

### Daily work

* Clone repository: `git clone REPO`
* Pick the feature/user-story to work out from the Board: say it is *#12345 - Integrate with billing server*
* Create a new branch with the following name convention: `feature/[#issue-id]_[feature_title-slug]` and move on it: `git switch -c feature/12345_integrate_with_billing_server`
* Working the issue, always add your changes to the stage using `git add -p` and interactively rewiewing all changes (this is important when code is autogenerated and can overwrite other's work: i.e. a Drupal Feature)
* Commit your code with a message following this naming convention: `[#issue-id]: Commit message`: `git commit -m '#12345: Admins can now store billing-id for a client'`
* Push it on a remote so that if your PC is blasted by aliens you can avoid being fired

### When your issue is done

* Fetch develop branch, keep integration branch fetched: `git fetch`
* Rebase your branch over develop: `git rebase origin/develop`
* Push to your branch: `git push -f` or better yet `git push -f origin feature/12345_integrate_with_billing_server`
* Gitlab flow: Head to Gitlab and open a Merge Request from your branch towards `develop`
* GitHub flow: Head to GitHub and open a Pull Request from your branch towards `develop`
* Address possible feedback in your branch and keep pushing over it
* When you are done the MR (or PR) will be merged by a peer or gatekeeper
* Switch back on `develop` and reset to the latest develop: `git fetch && git reset --hard origin/develop`

Redo from start and live happy! :)

## Pro-tips

* When you open a branch to work out a user-story, and have to name it against the naming convention we exposed, consider that the title part is amendable at need, the issue-id *is not!*
* When you create a new commit, try to keep your message short but significant! `#12345: More love` means nothing! A good rule of thumb is: don't write what you did (others can see the code by themselves) but *why you did it*
* If your work spans over a long time (days) we advice you rebase it onto develop at least daily: `git fetch && git rebase origin/develop` (solve conflicts if they arise and push with `-f` options).
* You can use an optional `-i` parameter when you rebase your branch onto develop, this way: `git rebase origin/develop`. In that case, you can pick only the commits you want to rebase, save and quit the interactive editor. Be warned: *there shall be dragons!*
* If you are working on a branch and you need to switch to another one, you can use `git stash` to save your work and `git stash pop` to restore it later
* If you don't see automated tools linting or testing the code while committing and pushing, please contact your team leader or the tech lead to setup the environment
* Please try to keep one commit per issue, and one issue per commit. This way, if you need to revert a commit, you can do it without reverting other's work

## Useful resources

* Force history rewriting on push: https://www.atlassian.com/git/tutorials/rewriting-history
* Interactive tutorials: https://ohmygit.org/ - https://learngitbranching.js.org/
* Gitlab flow: https://docs.gitlab.com/ee/topics/gitlab_flow.html
* GitHub interactive tutorial: https://skills.github.com/
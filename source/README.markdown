
Site source for [Kjuly.me](http://kjuly.me).

## USAGE

### Setup(alpha):

    git clone -b source git@github.com:Kjuly/kjuly.github.com.git kjuly.me
    # If not use multiple account to manage this repo, just use:
    # '# --- xxx' are settings for multiple account
    # ---git clone -b source git@github-another:anotherAccount/anotherAccount.github.com.git 0x6x # git@github.com -> git@github-another

    cd kjuly.me     # If you use RVM, You'll be asked if you trust the .rvmrc file (say yes)
    ruby --version  # Should report Ruby 1.9.2
    gem install bundler
    rbenv rehash    # If you use rbenv, rehash to be able to run the bundle command
    bundle install
    rake install    # Install the default Octopress theme

    # ---git config user.name "anotherUserName"
    # ---git config user.email "anotherAccount@example.com"

    # Initial commit of deploy will be the default(global) user setting
    git config --global user.name "Kjuly"
    git config --global user.email "email@example.com"

    rake setup_github_pages

    cd _deploy  # _delply has its own .git
    # ---git config user.name "anotherUserName"
    # ---git config user.email "anotherAccount@example.com"

    rake generate
    rake deploy

    # Set the default(global) user settings back to default user if have
    # ---git config --global user.name "Another User Name"
    # ---git config --global user.email "Another Email Address"

---
### Updating:

    git pull octopress master     # Get the latest Octopress
    bundle install                # Keep gems updated

If you’ve pulled in changes and you want to update your `/source` directory, run this.

    rake update_source            # update the template's source

If you’ve pulled in changes and you want to update your `/sass` directory, run this.

    rake update_style             # update the template's style

More refer it [HERE](http://octopress.org/docs/updating/).

---
### Blogging:

    rake new_post["Title"]

Then edit the post:

    vim soruce/_post/[the date]-TiTle.markdown

Local test:

    rake generate # Generates posts and pages into the public directory
    rake watch    # Watches source/ and sass/ for changes and regenerates
    rake preview  # Watches, and mounts a webserver at http://localhost:4000

Deploy to `master` branch :

    rake deploy

Git management for `source` branch:

    git add .
    git commit -m "New Post: Title"
    git push origin source

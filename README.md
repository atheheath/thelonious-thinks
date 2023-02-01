# Thelonious Thinks
Welcome! This is a website that I'm using to generically practice writing and communication. My partner thought it would be a good idea. She's smart.

[Link to Website](https://atheheath.github.io/thelonious-thinks/)

# Development
* To serve the website locally in dev mode:
    ```
    rvm use 3.1.3
    rvm gemset create thelonious-thinks
    rvm gemset use thelonious-thinks
    jekyll serve --source site/
    ```
### Note: You'll need to refresh the page in the browser for changes to take effect

# How I built the website

### Note I'm on a Mac M1 here, so somethings will obviously change for you depending on whatever you're using
There's a bunch of documentation out there that I was able to bumble around to make everything work. But at the end of the day, GitHub made it reaaaaaaal easy for me to make it happen. In short, here's what I did:
* [Created a new repo](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages)
* [Created Github Actions workflow to publish on push](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow) 
    * In the repo went to Settings -> (Under Code and automation on the left) Pages -> (Under Build and Deployment) Source = Github Actions -> Jekyll template -> Used default template
    * Changed template in [`jekyll-gh-pages.yml`](https://github.com/atheheath/thelonious-thinks/blob/main/.github/workflows/jekyll-gh-pages.yml) so that `jobs.build.steps.with.source = ./site`
* Installing new versions of ruby turned out to be a PAIIIIINNNNNN. I followed a hybrid of the famous [Nicky Marino](https://nickymarino.com/2021/12/17/install-ruby-273-on-m1/) and [this tutorial here](https://jekyllrb.com/docs/installation/macos/). I used `rvm` to install and build ruby and didn't use `ruby-install` nor `ruby-build` nor `rbenv` because I couldn't get them to work on Rosetta.
    * ```brew86 install chruby xz```
    * Had to make some changes to get these packages on the path
        ```bash
        echo '\n' >> ~/.zprofile`
        echo '# Ruby dependencies' >> ~/.zprofile`
        echo 'source '"$(brew86 --prefix chruby)"'/share/chruby/chruby.sh' >> ~/.zprofile` # (again, the homebrew path will most likely be different. To find out, use `brew86 --prefix chruby` and `brew86 --prefix ruby-install`, etc.)
        ```
    * [Install `rvm`](https://rvm.io)
        * Not writing it here because I'm sure some keys might change in the future
    * Now install the new ruby version
        ```bash
        export PATH="$(brew86 --prefix)/opt/openssl@1.1/bin:$PATH"
        export LDFLAGS="-L$(brew86 --prefix)/opt/openssl@1.1/lib"
        export CPPFLAGS="-I$(brew86 --prefix)/opt/openssl@1.1/include"
        export PKG_CONFIG_PATH="$(brew86 --prefix)/opt/openssl@1.1/lib/pkgconfig"
        
        rvm autolibs disable
        
        export RUBY_CFLAGS=-DUSE_FFI_CLOSURE_ALLOC
        export optflags="-Wno-error=implicit-function-declaration"
        
        rvm install 3.1.3 --with-openssl-dir=$(brew86 --prefix)/opt/openssl@1.1
        ```
    * [Create RVM Environment](https://fgimian.github.io/blog/2012/12/08/setting-up-virtual-development-environments-for-ruby/)
        ```bash
        rvm use 3.1.3
        rvm gemset create thelonious-thinks
        rvm gemset use thelonious-thinks
        bundle install
        ``` 
* Now create the site!
    ```bash
    jekyll new site/ --blank
    ```
* Make first edits at `site/index.md` and you're good to go!

# Possible Topics
* [Markdown tips and tricks](https://gist.github.com/clintel/1155906#file-gistfile1-md)
* [Attention is all you need](https://arxiv.org/abs/1706.03762)
* Tree vs. Network ML Models and signal inputs

# Todos
* I doubt anyone will actually read this blog, but how can we measure? https://clicky.com

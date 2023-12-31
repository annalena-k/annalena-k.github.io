Personal webpage of Annalena Kofler: [annalenakofler.com](https://www.annalenakofler.com)

# Tutorial: How to create your own website

Summary: The following tutorial explains “How to create a github website with Jekyll”

Prerequisites: Github account, NOT Windows

Since I encountered some challenges when trying to set up my own webpage, I documented my process in this tutorial that extends the cited standard tutorial of github. Additionally, I explain commonly used terms for people that are new to web development. If you find some steps difficult to follow or come across outdated or erroneous information, please contact me via email (firstname.lastname@tuebingen.mpg.de).

### Steps:

1. **Create first simple github website** 
Following https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site 
    - Each github user can create one webpage for which the repository has to be public.
    - Include initial, simple .md document so that you see the first look. (This might take up to 15 minutes until it is registered and can be accessed via `username.github.io`
    - However, this is not sufficient for a standard website → use Jekyll
2. **Set up Jekyll on your computer**
    - Install Ruby: [https://www.ruby-lang.org/en/documentation/installation/](https://www.ruby-lang.org/en/documentation/installation/#homebrew)
    - Install Bundler which provides a consistent environment for Ruby that trakcs and extracts all needed gems and versions: [https://bundler.io](https://bundler.io/)
    - Clone repository to local machine where Ruby and Bundler are installed
    - Install Jekyll via Bundler: https://jekyllrb.com/tutorials/using-jekyll-with-bundler/ where `my-jekyll-website` is github folder
        - If you use the standard install location of `gem install` and you do NOT configure the bundler install path, you can use `bundle add jekyll` to install jekyll. In this case, you can follow the commands in https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll?platform=mac directly.
        - If you change the bundler install path as described in https://jekyllrb.com/tutorials/using-jekyll-with-bundler/,  you have to use `bundle install --path vendor/bundle` instead. In this case, some commands in https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll?platform=mac might not work directly and you should prefix them with `bundle exec` so that Bundler runs the version of Jekyll that is installed in your project folder.
3. **Include Jekyll in github website**
Most of this step is based on: https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll?platform=mac
    - If not specified otherwise, the main branch will be used (you can configure the publishing source via https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site )
    - Navigate to your `username.github.io` folder in the terminal. If you specified another publishing source than the main branch, checkout the according branch.
    - If the github folder is empty, you can create a Jekyll site via `jekyll new --skip-bundle .` . If there is already some content present, e.g. some `README.md` file, you need to add the `--force` specifier: `jekyll new --force --skip-bundle .` (or `bundle exec jekyll new --force --skip-bundle .`)
    - (Now, we are at point 8 of “Creating your site” on [https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll?platform=mac](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll?platform=mac#creating-your-site) .)
    Open the `Gemfile` created by jekyll and comment out the line that starts with `gem "jekyll”`.
    - Add the github-pages gem by editing the line starting with # gem "github-pages". Change this line to:
        
        ```markdown
        gem "github-pages", "~> GITHUB-PAGES-VERSION", group: :jekyll_plugins
        ```
        
        where GITHUB-PAGES-VERSION has to be replaced with the latest supported version of the `github-pages`gem. You can find this version here: https://pages.github.com/versions/, e.g. in my case 228. This will ensure that the correct jekyll version for the `github-pages` gem will be installed.
        
    - Save and close the `Gemfile`.
    - Run `bundle install` in the command line. (Maybe you need to `bundle update` first.)
    - Edit the `_config.yaml` file. This file contains meta information of the webpage such as name, email, and description used in google searches. If the webpage is hosted in a subdirectory, this has to be specified here.
    You can search for a github page from someone else that you can use as an inspiration.
    - Add `.bundle/` to `.gitignore` file. (`vendor/` should be included automatically, but check this!)
    Example for `.gitignore` file from https://jekyllrb.com/tutorials/using-jekyll-with-bundler/
        
        ```markdown
        # Ignore metadata generated by Jekyll
        _site/
        .sass-cache/
        .jekyll-cache/
        .jekyll-metadata
        
        # Ignore folders generated by Bundler
        .bundle/
        vendor/
        ```
        
    - Commit and push your changes
    - Go to `username.github.io` to have a first look.
4. **Editing the website** (and making it more beautiful 🤩)
    - General Setup: The base Jekyll theme is built based on pages and posts.
    - Pages
        - Used for content that does not change over time and that is not a group of content (such as staff members or recipes)
        - Can be created by adding an HTML file (or Markdown file that is converted to HTML by a front matter on build) in the root directory, default example `about.markdown`
        - More information: https://jekyllrb.com/docs/pages/
    - Posts
        - Used for blog posts that are associated with a specific date
        - Saved in `_posts/` folder with example `2023-10-19-welcome-to-jekyll.markdown`
        - New post can be created by adding new file with filename format `YEAR-MONTH-DAY-title.MARKUP` in `_posts/` folder
        - All post files must begin with a front matter which specifies the layout and meta data
        example from https://jekyllrb.com/docs/posts/:
            
            ```markdown
            ---
            layout: post
            title:  "Welcome to Jekyll!"
            ---
            
            # Welcome
            
            **Hello world**, this is my first Jekyll blog post.
            
            I hope you like it!
            ```
            
        - More information: https://jekyllrb.com/docs/posts/
5. Use your own **custom domain** instead of the standard `[username.github.io](http://username.github.io)` and verifying it with github https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages
The github explanation was not very clear to me and I found it hard to follow some steps due to a lack of detail. Therefore, the following steps extend the github tutorial.
A better reference is https://stackoverflow.com/questions/9082499/custom-domain-for-github-project-pages
    - Buy your desired domain via a service of your choice
    - Go to your `github.io` folder, click ‘Settings’ at the top menu bar, and select ‘Pages’ which is listed under ‘Code and automation’. If you scroll down, you will find ‘Custom Domain’.
    - Enter your own domain below ‘Custom Domain’ and click save. As a result, it will tell you that a DNS Check is in progress. DNS stands for ‘domain name system’ which is responsible for linking domain names such as `username.github.io` to their internet protocol (IP) addresses which allows the browser to access the website. 
    In the DNS check, github looks up your custom domain on the domain name servers to see whether it exists and whether is configured correctly such that github can access it to display your newly created website. 
    With this step, github automatically creates a CNAME file in your github repository that contains the custom domain. If you pull these changes from the remote repository, you can check the file.
    - At the moment, your custom domain is not configured correctly and if you visit your custom domain in the browser, a warning from the company where you bought the domain might be shown. Probably, it says something like ‘Sorry, this domain is already taken. If you own this domain, login here.’
    - In order to configure your custom domain, you need to login to the DNS provider’s web portal. Navigate to the settings where you see the DNS records. It might be the case that some DNS records are already set by default that point to the company’s ‘domain is already taken’-website. You have to delete the corresponding records before replacing them with the new github record. (If an old record is not deleted, DNS conflicts can occur resulting in the github page not being shown.)
    - There are three types of DNS records that are important here: ‘A’, ‘AAAA’, and ‘CNAME’.
        - A’-type records are responsible for redirecting `your-domain.com` to `www.your-domain.com` or vice versa for IPv4.
        - ‘AAAA’-type DNS records do the same as ‘A’-type records, but for IPv6. Since the use of IPv6 is increasing, it is recommended to configure both.
        - ‘CNAME’-type DNS records point `www.your-domain.com` to any other domain, in our case the `username.github.io` webpage.
    - In the following, we will go through all three types. Although the order of configuring them should be irrelevant, it mattered in my case due to DNS conflicts. I will follow the order that worked for me. For each DNS record, you can specify the TTL which is the ‘time-to-live’ and refers to the time in seconds for which the data package is cached until it is automatically refreshed. Usually, you do not have to change the default value which is often 1h. After saving the DNS entry, you need to wait for the changes to propagate through the DNS name server which takes at least the specified TTL.
    - Configuring the ‘A’-type DNS records:
        - Go to the DNS record settings of your provider’s website portal.
        - If some ‘A’ record is already specified, delete it.
        - Create your new ‘A’-type DNS record:
        For some DNS providers, you have to specify directing @ (called ‘root apex’) to the github IP addresses, for others you have to leave the domain field blank. In total, four root apices have to be directed to four github IPv4 addresses which are listed here [https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-a-records-with-your-dns-provider](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain) at point 5 of “Configuring an apex domain”.
        At the time of writing, they are
            
            ```markdown
            185.199.108.153
            185.199.109.153
            185.199.110.153
            185.199.111.153
            ```
            
        - In the end, you should have four individual ‘A’-type records pointing to the four github IPv4 addresses.
    - Configuring the ‘AAAA’-type DNS records:
        - Go to the DNS record settings of your provider’s website portal.
        - If some ‘AAAA’ record is already specified, delete it.
        - Create your new ‘AAAA’-type DNS record:
        For some DNS providers, you have to specify directing @ (called ‘root apex’) to the github IP addresses, for others you have to leave the domain field blank. In total, four root apices have to be directed to four github IPv6 addresses which are listed here [https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-a-records-with-your-dns-provider](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain) at point 5 of “Configuring an apex domain”.
        At the time of writing, they are
            
            ```markdown
            2606:50c0:8000::153
            2606:50c0:8001::153
            2606:50c0:8002::153
            2606:50c0:8003::153
            ```
            
        - In the end, you should have four individual ‘AAAA’-type records pointing to the four github IPv6 addresses.
    - Configuring the ‘CNAME’-type DNS record:
        - Go to the DNS record settings of your provider’s website portal.
        - If some ‘CNAME’ record is already specified, delete it.
        - Create your new ‘CNAME’ DNS record:
        The DNS record should point `www.your-domain.com` to the `username.github.io` webpage. (Important: The github username is not necessarily the name of the github repository, but your real github username.)
    - Finally, you can check your configurations.
        - You can check CNAME by typing `dig www.your-domain.com +nostats +nocomments +nocmd` in the terminal which should return something like
            
            ```markdown
            www.your-domain.com.	2895	IN	CNAME	username.github.io.
            ```
            
        - You can confirm the ‘A’-type DNS entries by typing `dig +noall +answer www.your-domain.com` or `dig your-domain.com +noall +answer -t A` in the terminal which should list the github IP addresses, e.g.
            
            ```markdown
            username.github.io.	2895	IN	A	185.199.110.153
            username.github.io.	2895	IN	A	185.199.111.153
            username.github.io.	2895	IN	A	185.199.108.153
            username.github.io.	2895	IN	A	185.199.109.153
            ```
            
        - You can check the ‘AAAA’-type entries with `dig your-domain.com +noall +answer -t AAAA` which should be similar to the output of the ‘A’-type check.
    - After the DNS check is successful, you should be able to access `www.[your-domain.com](http://your-domain.com)`  as well as `your-domain.com` and see your new github page.
    - It is highly recommended to enforce **https** for your webpage which can be done by clicking the checkbox ‘Enforce https’ below the custom domain. If you have issues, refresh the webpage or ask the github chatbot for help as detailed here https://github.com/orgs/community/discussions/23049
    - It might be the case that you need to verify your domain for github pages: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages

My website is inspired by [Heiner Kremer's webpage](https://github.com/HeinerKremer/heinerkremer.github.io).

# this-is-a-repo [![Build Status](https://travis-ci.org/Geo1088/this-is-a-repo.svg?branch=master)](https://travis-ci.org/Geo1088/this-is-a-repo)

## To use

- Have a Reddit API application of type "script" (There are tutorials on this elsewhere, but I'm too lazy to link them)
- Add your repo to [Travis CI](https://travis-ci.org/)
- Copy `.travis.yml` and the `.update` directory into the root of your repo
- From your repo's settings in Travis, add `REDDIT_CLIENT_ID`, `REDDIT_CLIENT_SECRET`, `REDDIT_USERNAME`, and `REDDIT_PASSWORD` as environment variables with the relevant information
- Edit `main.scss`, commit your code, and push to GitHub
- Wait for the Travis build to finish and check out your sub!
 
## Advanced configuration

### Linking multiple subreddits

The update script can take a subreddit name as an argument, which means that you can set up your `.travis.yml` deployments to work with multiple subreddits. For example, you could link one branch of your repository to your main sub and another to a private staging sub, you could use the following `.travis.yml` deploy config:

```yml
deploy:
- provider: script
  script: python .update/updateSubreddit.py mainSubreddit
  skip_cleanup: true
  on:
    branch: master
- provider: script
  script: python .update/updateSubreddit.py stagingSubreddit
  skip_cleanup: true
  on:
    branch: staging
```

If arguments are passed to the script in this manner, the `REDDIT_SUBREDDIT` environment variable will be ignored.

### Skipping minification

By default the script minified the compiled output before sending it to your subreddit. However, if you'd like to maintain whitespace in your compiled CSS, you can add a `REDDIT_SKIP_MINIFY` environment variable to your Travis configuration and set it to anything other than `0` or `false`.

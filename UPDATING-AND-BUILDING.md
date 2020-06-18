# Updating the library from Google's master branch and building for node

## Setting up the environment

Follow all the necessary steps described in [Javascript README](javascript/README.md)
Make sure all cloned projects are at the same folder level (siblings) as this project.

Snippet taken from the document for quick reference:
> * `git clone https://github.com/google/libphonenumber/`
>
> * `git clone https://github.com/google/closure-library/`
>
> * `git clone https://github.com/google/closure-compiler.git`
>
> * `git clone https://github.com/google/closure-linter.git`
>
> * `git clone https://github.com/google/python-gflags.git`



**Note:** If you face any gwt related errors on closure compiler during build later on update the version of gwt-user & gwt-dev to 2.8.2
```
    <dependency>
      <groupId>com.google.gwt</groupId>
      <artifactId>gwt-user</artifactId>
      <version>2.8.2</version>
    </dependency>

    <dependency>
      <groupId>com.google.gwt</groupId>
      <artifactId>gwt-dev</artifactId>
      <version>2.8.2</version>
    </dependency>
```

Inside libphonenumber project also add upstream
```
git remote add upstream https://github.com/google/libphonenumber.git
```

## Building and updating process

Current master is set to be identical with the official google repo it was cloned from (upstream).
All changes in lib are going on `js/node-module` branch


### Updating master from upstream
Make sure you are on master
```
git checkout master
```
Fetch new code changes from upstream
```
git fetch upstream
```
Merge the new code to master
```
git merge upstream/master
```

Checkout node branch and rebase node branch from master and resolve any conflicts
```
git checkout js/node-module
git rebase --onto origin/master <previous latest master commit id here>
```

### Build with new changes from upstream
Checkout node branch 
```
git checkout js/node-module
```
Run npm build task
```
npm run build
```


### Publishing to npm
Login to npm
```
npm login
```

Publish
```
npm publish --access public
```
# beeware-tutorial

Following [this tutorial](https://docs.beeware.org/en/latest/index.html).

## [Step 0](https://docs.beeware.org/en/latest/tutorial/tutorial-0.html)

## [Step 1](https://docs.beeware.org/en/latest/tutorial/tutorial-1.html)

## [Step 2](https://docs.beeware.org/en/latest/tutorial/tutorial-2.html)

## [Step 3](https://docs.beeware.org/en/latest/tutorial/tutorial-3.html)
Didn't include any code changes, so taking a not here.

`briefcase create` creates application scaffolding to support the packaging process.
- Generated application template
- Dowloads and installs supporting packages
- Installs app requirements
- Installed your app code
- Installed your resources (icons, etc.)

`briefcase build` creates the exe after compilation and metadata updates.

`briefcase run` will run that exe instead of running python / dev environment.

`briefcase package` will turn that into an msi.

## [Step 4]()
`briefcase dev` runs your code as is.
`briefcase run` runs your built app, so it needs updated.
`briefcase update` will do that so that we don't have to start from scratch or manually delete anything.

Then there is this:
> Now that we’ve updated the installer code, we can then run `briefcase build` to re-compile the app, `briefcase run` to run the updated app, and `briefcase package` to repackage the application for distribution.

- Instead, I ran `run` and got the updated version; is `build` needed after `update`?

- To test, I ran `package` and installed the app over my existing version that I installed (old, no popup).
 - That produced the expected result!

`briefcase run [-u/--update]` to troubleshoot/iterate the built version quickly.
`briefcase package -u` to make a change to the app before re-packaging.

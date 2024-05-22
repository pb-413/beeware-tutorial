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

## [Step 5](https://docs.beeware.org/en/latest/tutorial/tutorial-5/index.html)

-> [Android](https://docs.beeware.org/en/latest/tutorial/tutorial-5/android.html)
-> [iOS](https://docs.beeware.org/en/latest/tutorial/tutorial-5/iOS.html)

## [Step 6](https://docs.beeware.org/en/latest/tutorial/tutorial-6.html)

Easy to go to web too!
And without any other steps, you can call `briefcase run web`!

## [Step 7](https://docs.beeware.org/en/latest/tutorial/tutorial-7.html)

Add requirement in development:
- `python -m pip install httpx`
- `briefcase dev`

Add requirement for builds:
- pyproject.toml > `[tool.briefcase.app.helloworld]` > `requires = []` > add pip installable package name
- `briefcase update -r` (update with new requirements), `build`, `run`

Ran into unreliably reproducible issue mentioned in this thread: [beeware/briefcase - Discussion 1404](https://github.com/beeware/briefcase/discussions/1404); contributed.

## [Step 8](https://docs.beeware.org/en/latest/tutorial/tutorial-8.html)
`def` -> `async def`
`httpx.Client()` -> `httpx.AsyncClient()`
`with` (context manager) -> `async with`
`client.get(...)` -> `await client.get(...)` (release to system)

## Interesting / Curious Stuff

(!) installing a new build msi results in the application appearing twice in the Apps > Installed apps list.


## Issues and Solutions

Ran out of hard drive space while `[android_sdk] Downloading the 'system-images;android-31;default;x86_64' Android system image...`
-> Found similar error on [beeware/briefcase - issue 1388](https://github.com/beeware/briefcase/issues/1338); mentioned that the steps there helped me

Ran into another error about storage space :(
```
[android_sdk] Emulator output log for startup failure
INFO    | Storing crashdata in: C:\Users\patby\AppData\Local\Temp\\AndroidEmulator\emu-crash-34.2.14.db, detection is enabled for process: 21232
INFO    | Android emulator version 34.2.14.0 (build_id 11834374) (CL:N/A)
INFO    | Found systemPath C:\Users\patby\AppData\Local\BeeWare\briefcase\Cache\tools\android_sdk\system-images\android-31\default\x86_64\
WARNING | Please update the emulator to one that supports the feature(s): Vulkan
WARNING | Failed to process .ini file C:\Users\patby\.android\avd\..\avd\beePhone.avd\quickbootChoice.ini for reading.
ERROR   | Not enough space to create userdata partition. Available: 5655.476562 MB at C:\Users\patby\.android\avd\..\avd\beePhone.avd, need 7372.800000 MB.
INFO    | Storing crashdata in: C:\Users\patby\AppData\Local\Temp\\AndroidEmulator\emu-crash-34.2.14.db, detection is enabled for process: 8404
INFO    | Duplicate loglines will be removed, if you wish to see each individual line launch with the -log-nofilter flag.
INFO    | Increasing RAM size to 2048MB
```
-> Found similar issue on [stack](https://stackoverflow.com/questions/53931877/emulator-emulator-error-not-enough-space-to-create-userdata-partition) with possible solution to bring emulation to D:\ drive which I have.
 -> That didn't work
 -> Moved things back around
-> Moved the BeeWare Cache to my D:\ drive via [env var config](https://briefcase.readthedocs.io/en/stable/reference/environment.html)
 -> Deleted more files (~5-6GiB temp)
 -> Booted!

# Heroku NX Monorepo Buildpack

In a [Nx Monorepo](https://nx.dev/) you can have multiple apps and libraries. Unfortunatly it is not as easy to deploy these apps to heroku as they are placed in subdirectories of one big Git repository. It is created to allow a flexible handling of multiple apps in a Nx Monorepo while keep Nx tooling like code change detection etc. intact. So each app is only deplyoed if the app has changed.

This buildpack is based on [lstoll/heroku-buildpack-monorepo](https://github.com/lstoll/heroku-buildpack-monorepo) and [omofolarin/nx-workspace-buildpack](https://github.com/omofolarin/nx-workspace-buildpack).

# Idea

On each commit to you selected Heroku App the following process will start:

1. The hole monorepo is copied to a tmp filder.
2. NPM install will add all dependencies.
3. The system checks if the app configured is affected by the last commit.
4. If it is affeced it is build.
5. The dist artifact is copied to the heroku root execution folder.
6. The app is started.

# Usage

1. Add a Procfile to the root dir of the app that shall be deplyoed.
2. Create a heroku app.
3. Add the relative path to your app `APP_BASE=relative/path/to/app/root`
4. Add the NodeJs Buildpack as it is needed by Nx and most likely the app does need it as well.
5. Add this buildpack `heroku buildpacks:add -a <app> https://github.com/polkemon/heroku-buildpack-nx-monorepo`
6. Connect your Git Monorepo (or push it manually).
7. Build and check the result.

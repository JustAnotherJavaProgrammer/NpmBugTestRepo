# Try it for yourself!

This is a demonstration repo for this [npm issue](https://github.com/npm/cli/issues/6893).

Here are two scenarios where the unexpected behavior occurs:

## Scenario 0: Setup

Before trying each scenario, please make sure that you have run `npm install` and there are no further local changes (reset after trying scenario 1).

You can see which branch is installed by checking the name of the file inside `node_modules/@proj/source`, which is either `main.branch` or `dev.branch`.

## Scenario 1: Changing the dependency

1. Change `package.json` to depend on the `dev` branch (`#dev` instead of `#main`). Don't forget to save the file.
2. Run `npm install`
3. Check for the currently installed branch. It will still be `main.branch`.

### Deleting `node_modules` does not fix this

For these steps, follow at least step 1 from above.

*Weirdly, this happens before and after running `npm install` in step 2 above.*

1. Delete the `node_modules` directory.
2. Run `npm install`.
3. As you will see, `main.branch` is present again, even though we just reinstalled all packages (caching issue?)
   For this behavior, the branch referenced in `package-lock.json` doesn't matter.

## Scenario 2: Changing the branch

1. Switch to the `depends-on-dev` branch.
2. Run `npm install`
3. Check for the currently installed branch. It will still be `main.branch`.

*Again, deleting `node_modules` does not fix this.*
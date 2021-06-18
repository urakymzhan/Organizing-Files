---

Organizing Files

---

The project is starting to grow in size. This is a point when some organization would help you manage and grow your application.

## Components

Components are self contained and represent UI elements. When possible you'd like your components to be portable. That is you'd like to take the components with you to new places so you don't have to write them over and over again each time you need a button or a nav bar.

In some cases a component will be very specific to a project. The `PLACESDetails` component is very specific to this project. The `Title` component on the other hand could be used anywhere.

In order to be portable a component might have other files that it requires. For example the `Title` Component imports `Title.css` and `NavLink` from `React Router Dom`.

### Grouping Dependencies

Organizing components and their dependencies in folders is one way to keep components organized and portable.

> [action]
>
> Create a new folder in the `src` folder name it `components`.
>
> Move all of your components into this folder. It should include all of the following files:
>
```
- src
  - App.css
  - App.js
  - App.test.js
  - components
    - About.js
    - PLACESDetails.js
    - PLACESList.css
    - PLACESList.js
    - PLACESSpace.css
    - PLACESSpace.js
    - serviceWorker.js
    - setupTests.js
    - Title.css
    - Title.js
  - index.css
  - index.js
```
>

All of your components should now be in the `components` folder, **except for index.js and index.css**. After this change, your folder structure should look like the following:

- src
  - components
    - About.js
    - App.css
    - App.js
    - App.test.js
    - PLACESDetails.js
    - PLACESList.css
    - PLACESList.js
    - PLACESSpace.css
    - PLACESSpace.js
    - Title.css
    - Title.js
  - index.css
  - index.js
  - serviceWorker.js
  - setupTests.js
  - places-data.json

This change broke the app! You should see this error on the browser:

> Failed to compile
>
> ./src/App.js
>
> Error: Module not found: Can't resolve ./App ...

This is telling us that the system can't find `App.js`. This would make sense since we moved it to a new location.

> [action]
>
> Open `index.js`. Notice that App is imported here.
>
> `import App from './App';`
>
> This line is no longer correct since App is now located in `src/components`. Changes this to:
>
> `import App from './components/App';`

That's fixed but there is another error:

> Failed to compile
>
> ./src/components/PLACESDetails.js
>
> Module not found: Can't resolve './places-data.json' in ...

This message is telling us that the Component `PLACESDetails.js` failed to compile because it can't find `./places-data.json`. This would make sense since `PLACESDetails.js` is in the components folder and `places-data.json` is in src.

> [action]
>
> Open `src/PLACESDetails.js`. Find the import statement near the top:
>
> `import data from './places-data.json'`
>
> Change this to:
>
> `import data from '../places-data.json'`

The difference here is pretty subtle. The difference is `./` vs `../`. This is a big difference. `./` indicates the current directory/folder. `../` indicates the parent directory/folder.

From here there's another error, but it's a different error so you are making progress.

> Failed to compile
>
> ./src/components/PLACESList.js
>
> Module not found: Can't resolve './places-data.json' in ...

This time the error is in `PLACESList.js` and it can't resolve `./places-data.json`. Sounds like we need to fix the path to `places-data.json` again!

> [action]
>
> Open `PLACESList.js`. Find the import statement at the top.
>
> `import data from './places-data.json'`
>
> Change `./` to `../`
>
> `import data from '../places-data.json'`

With these changes, you should have everything working in the example project. You might have to refresh the browser page after these changes.

### Grouping Components

Components can be grouped in folders. Often you had a component that was made of a JS and a CSS file. Putting these in the same folder will group these together.

Moving the files into new folders will create errors in your import statements that you will need to fix.

> [action]
>
> Make a folder for each of the Components you created and move that component and its CSS file into the folder. **Give the folder the same name as the component**. Be sure to fix the errors and import statements as needed.

After these changes, your `src` directory should look like this:

- src
  - components
    - About
      - About.js
    - App.css
    - App.js
    - App.test.js
    - PLACESDetails
      - PLACESDetails.js
    - PLACESList
      - PLACESList.css
      - PLACESList.js
    - PLACESSpace
      - PLACESSpace.css
      - PLACESSpace.js
    - Title
      - Title.css
      - Title.js
  - index.css
  - index.js
  - serviceWorker.js
  - setupTests.js
  - places-data.json

Note you will need to update your imoport statements after moving your files. This includes statements that import the component into `App.js` and places where you may have imported `places-data.json`.

# Now Commit

> [action]

```bash
$ git add .
$ git commit -m 'organizing files'
$ git push
```


#### File Structure
For a default project, the file structure looks like this:
- `app.json`: Contains config options for the project; changes behaviour of project 
- `babel.config.json`: Extends default preset (predefined content block); Adds support for decorators, tree-shaking web packages, loading font icons etc.
- `package.json`: Project's dependencies, scripts and metadata
- `tsconfig.json`: TypeScript rules to enforce type safety
- `scripts/`: contains reset-project.js which will save current state of app folder, then erase it's contents
- `hooks/`: allows sharing common behavior between components
- `constants/`: color.ts which contains a list of color values throughout the app.
- `components/`: React Native components
- `assets/`: contains images for app
- `app/`: determines the app's navigation
	- The app has two screens: **app/(tabs)/index.tsx** and **app/(tabs)/explore.tsx**. The layout file in **app/(tabs)/\_layout.tsx** sets up the tab navigator.


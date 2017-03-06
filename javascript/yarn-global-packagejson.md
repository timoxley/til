# yarn global package.json

Unlike `npm`, `yarn` keeps a list of all globally packages and their versions in a `package.json`.

e.g.

```
> cat ~/.config/yarn/global/package.json
{
  "dependencies": {
    "babel-eslint": "^7.1.1",
    "create-react-app": "^1.0.3",
    "docker-run": "^3.0.0",
    "eslint": "3.15.0",
    "flow-bin": "^0.40.0",
    "getstorybook": "^1.7.0",
    "googleauth": "^3.0.2",
    "gulp": "latest",
    "hotel": "^0.5.13",
    "lerna": "latest",
    "linklocal": "^2.8.0",
    "next": "^1.2.3",
    "npm-check-updates": "^2.8.9",
    "npm-idempotent-rebuild": "^1.0.2",
    "npm-run": "^4.1.0",
    "pkgfiles": "^2.3.2",
    "standard": "^8.6.0",
    "webpack": "*",
    "yarn": "^0.20.3"
  }
}
```

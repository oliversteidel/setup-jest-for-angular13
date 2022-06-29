# How to setup Jest in Angular in 10(!!!) easy steps

## 1. remove Jasmine & Karma

```
npm uninstall @types/jasmine jasmine-core karma karma-chrome-launcher karma-coverage karma-jasmine karma-jasmine-html-reporter
```

## 2. remove "test" from angular.json

```json
"test": {
          "builder": "@angular-devkit/build-angular:karma",
          "options": {
            "main": "src/test.ts",
            "polyfills": "src/polyfills.ts",
            "tsConfig": "tsconfig.spec.json",
            "karmaConfig": "karma.conf.js",
            "inlineStyleLanguage": "scss",
            "assets": ["src/favicon.ico", "src/assets"],
            "styles": ["src/styles.scss"],
            "scripts": []
          }
        }
```

## 3. delete file: karma.conf.js

<br>

## 4. delete file: test.ts

<br >

## 5. install Jest to dev-dependencies

```
npm install jest @types/jest jest-preset-angular --save-dev
```

## 6. create file "setup.jest.ts"

```ts
import 'jest-preset-angular/setup-jest';
```

## 7. update tsconfig.spec.json

```json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "outDir": "./out-tsc/spec",
    "types": ["jest", "node"]
  },
  "files": ["src/setup.jest.ts", "src/polyfills.ts"],
  "include": ["src/**/*.spec.ts", "src/**/*.d.ts"]
}
```

## 8. update package.json - modify "scripts" and add "jest"

```json
"scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "watch": "jest --watch",
    "test": "jest"
},
"jest": {
    "preset": "jest-preset-angular",
    "setupFilesAfterEnv": [
      "./src/setup.jest.ts"
    ],
    "testPathIgnorePatterns": [
        "<rootDir>/node_modules/",
        "<rootDir>/dist/"
    ],
    "globals": {
        "ts-jest": {
            "tsConfig": "<rootDir>/tsconfig.spec.json/",
            "stringlifyContentPathRegex": "\\.html$"
        }
    }
}
```

## 9. replace jasmine syntax in the existing \*.spec.ts test files with jest

# Repro

## Root Cause
I believe the reason WebStorm cannot tell if we are using the legacy versions of angular material 
components is due to our project structure, in which modules from Angular Material are exported by
one of our internal component libraries. In this example, I made a minimal reproduction by creating a
multi-project Angular workspace, one project is an Angular library (`projects/components`), the other
is a test app (`projects/repro`).

## Steps to Repro

1) First, make sure you build the `components` library found under `projects/components` by running:
```
ng build --project=components
```

2) Then, open up the file `projects/repro/src/app/app.component.html` in WebStorm (Build #WS-231.8770.64). You will notice that the material components are marked as deprecated.

3) Use middle-mouse click on the tag `<mat-card>`, you will notice that there are two definitions that WebStorm sees in `node_modules`, one is the legacy definition, the other is the current.

## Project Structure
In `projects/repro/src/app/app.module.ts`, I am importing a module from the `projects/components` 
named `MaterialComponentsModule` (line 6). That is how the app is importing in the 
components we wish to use, we export everything we wish to use from `MaterialComponentsModule` found
in the components library under `projects/components/src/lib/material-components/material-components.module.ts`.

 


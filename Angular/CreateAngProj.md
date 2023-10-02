# In terminal (GitBash):

1.  Navigate to Folder
2.  ng new [name_of_project] **no brackets*
   >if strict mode, add --no-strict (after name_of_project)

    1.  enter
    2.  ?1 - N
    3.  ?2 - CSS
3.  cd into [name_of_project] **no brackets*
4.  Once in project, run:
    1.  npm i bootstrap@latest 
    2.  code .    **opens in vs code*


# In VS Code:

1.  angular.json file
    1.  Syles array, add:
        1.  "node__modules/boostrap....min.css"

## Within app file:

1.  remove test file (spec file)
2.  delete everything in HTML
3.  ADD:
    1.  <h1>Hello, World</h1>
    2.  run ng serve, open localhost:4200

## Generate new components (w/i app)

run ng (angular) g (generate) c (component) [**name of component* ... no brackets]

> i.e.:  ng g c [**name of new component* ... no brackets]
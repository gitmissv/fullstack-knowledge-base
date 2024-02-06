# Services in Angular

- Services help manage your program data and provide a way to share information among classes, within your project, that don't 'know each other' or aren't naturally connected.
- A service is a simple TypeScript class *(i.e.: TravelList.service.ts)*
- Services help to clean up your code to create less code with same functionality.
- You can create services in the main app folder --or-- create/add within a shared folder w/i main app folder
- Naming convention is typically the **why** of creating the service (to be explicit about what the service does)
- 

## Dependency Injector

- Add constructor() where you want to add your service
- Import your service @ top, then add your constructor()
  - > note that your constructor will include name of service *(without '.')* as both the name AND the type.
  - > i.e.: constructor(private TravelListService: TravelListService) {}


## Hierarchial Injector Services

- Services provide data to child components only
- Services do **NOT** propogate up ... only down the 'tree'
- > you can still use the data, but you cannot add as a provider
- > HIGHEST possible level is app.Module.ts - where you can import and add providers.


# Create a new Service in Angular:

- ng g service [name] **no brackets*
    > this creates your skeleton as [name].service.ts

- Add to your new service:
  - Import { Injectables } from '@angular/core';

  - @Injectable({ providedIn: 'root',
    - }) 
  - export class [name]Service {
      - constructor() { } 
    - }

**NOTE** this '@Injectable...' is similar to the '@Component...' in other app modules.
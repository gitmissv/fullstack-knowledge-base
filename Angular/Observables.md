# Observables - RxJS
 - store your data source

How to handle (3 ways):

  DATA  ---->  ERROR  ---->  COMPLETION

  -------------Observer----------------


## INSTALL RxJS v6:

    > npm install --save rxjs@6

 - Also install rxjs-compat pkg:

    > npm install --save rxjs-compat 


Observables are constructs you subscribe to, to be informed about changes in your data
 - this.route.params.subscribe(.....)


i.e.:
ngOnInit() {
    this.route.params.subscribe(next: (params:Params) => {
        this.id= +params.id;
    })
}

    > If subscribing to something that counts (i.e.: interval) thru rxjs --->> be sure to unsubscribe using OnDestroy
    ---
    ---
    ---then ...
    ngOnDestroy(): void {
        this.[name of subscribe].unsubscribe(); 
    }


# Observables -> rxjs library

Built-in Operators
 > import { ...  } from 'rxjs/operators';

  - all use 'pipe' (to add one ore more operators)
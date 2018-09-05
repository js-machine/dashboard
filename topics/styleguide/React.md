# React styleguide

For more information about react use official docs https://reactjs.org/

## Table of Contents

* [File system structure](#file-system-structure)
* [Basics](#basics)
    * [Mixins](#mixins)
    * [Naming](#naming)
    * [Alignment](#alignment)
    * [Quotes](#quotes)
    * [Spaces](#spaces)
    * [Props](#props)
    * [Refs](#refs)
    * [Tags](#tags)
    * [Methods](#methods)
* [Redux](#redux)
    * [Actions](#actions)
    * [Effects](#effects)
    * [Reducer](#reducer)

## File system structure

* Use `components+scenes` folder structure for components and views (all views are placed in ‘scenes’ folder and has own components, but common components are placed in another folder - ‘components’ - outside the scenes).

###

    src
    ├── components
    ├── scenes
    ├── services
    ├── models
    ├── ...
    ├── store
    ├── App.tsx
    ├── index.tsx
    └── README.md

* Good practice for components to have separate folder. 

###
    src
    ├── components
        ├── CaButton
            ├── CaButton.tsx
            ├── CaButton.css/less/scss
            ├── CaButton.models.ts/interfaces.ts/types.ts
            ├── index.ts
        ├── index.ts
    ├── ...

## Basics

* Use `class extends React.Component` instead of `React.createClass`

    ```tsx
    /*Bad*/

    const Listing = React.createClass({
        render() {
            return (<div>{this.state.hello}</div>);
        }
    });
    ```

    ```tsx
    /*Good*/

    class Listing extends React.Component {
        public render(): JSX.Element {
            return (<div>{this.state.hello}</div>);
        }
    }
    ```

* Always use `()` in render function

    ```tsx
    /*Bad*/

    class Listing extends React.Component {
        public render(): JSX.Element {
            return <div>{this.state.hello}</div>;
        }
    }
    ```

    ```tsx
    /*Good*/

    class Listing extends React.Component {
        public render(): JSX.Element {
            return (<div>{this.state.hello}</div>);
        }
    }
    ```

### Mixins
* Don't use [mixins](https://reactjs.org/blog/2016/07/13/mixins-considered-harmful.html)

    *Why?* Mixins make implicit dependencies, cause conflicts of names and rapid growth of complexity.

### Naming
* Don't use `default` in export
* Extensions: Use .jsx/.tsx file extension for React components.
* Files: Use `PascalCase`, example `DataList.tsx`.
* Variables: Use `PascalCase` for React components and `camelCase` for it instances

    ```ts
    /*Bad*/
    import reservationCard from './ReservationCard';

    /*Good*/
    import ReservationCard from './ReservationCard';

    /*Bad*/
    const ReservationItem = <ReservationCard />;

    /*Good*/
    const reservationItem = <ReservationCard />;
    ```

* Components: Use file naming as well as the components.

    ```ts
    /*Bad*/
    import Footer from './Footer/Footer';

    /*Bad*/
    import Footer from './Footer/index';

    /*Good*/
    import Footer from './Footer';
    ```

* Properties: Avoid usage of DOM-components for different purposes. For example if we need to define a new input we shouldn't override standart properties such as `style` or `className`

    ```tsx
    /*Bad*/
    <MyComponent style="fancy" />

    /*Bad*/
    <MyComponent className="fancy" />

    /*Good*/
    <MyComponent variant="fancy" />
    ```

### Alignment

* Use the following styles:

    ```tsx
    /*Bad*/
    <Foo superLongParam="bar"
        anotherSuperLongParam="baz" />

    /*Good*/
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />

    /*If the properties are placed in one line, leave them as they are*/
    <Foo bar="bar" />

    /*Indentation of child elements is specified as usual*/
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    >
      <Quux />
    </Foo>
    ```
### Quotes

* Always use double quotes `"` for JSX-attributes and single `'` for others

    *Why?* For standard HTML attributes double quotes are usually used, not single ones. JSX attributes also follow this convention.

    ```tsx
    /*Bad*/
    <Foo bar='bar' />

    /*Good*/
    <Foo bar="bar" />

    /*Bad*/
    <Foo style={{ left: "20px" }} />

    /*Good*/
    <Foo style={{ left: '20px' }} />
    ```

### Spaces

* Use `2` spaces 

    *Why?*: More JS teams do it (e.g. [npm](https://github.com/npm/npm), [node](https://github.com/nodejs/node), [google/angular](https://github.com/angular/angular/), [facebook/react](https://github.com/facebook/react)). The TypeScript/VSCode teams use 4 spaces but are definitely the exception in the ecosystem.

* Always insert one space in your self-closing tag

    ```tsx
    /*Bad*/
    <Foo/>

    /*Bad*/
    <Foo                 />

    /*Bad*/
    <Foo
    />

    /*Good*/
    <Foo />
    ```

* Do not separate braces with spaces in JSX

    ```tsx
    /*Bad*/
    <Foo bar={ baz } />

    /*Good*/
    <Foo bar={baz} />
    ```

### Props

* Use `camelCase` for props naming

    ```tsx
    /*Bad*/
    <Foo
      UserName="hello"
      phone_number={12345678}
    />

    /*Good*/
    <Foo
      userName="hello"
      phoneNumber={12345678}
    />
    ```

* Destructure your props

    *Why?*: It makes code more cleaner and readable

    ```tsx
    /*Bad*/

    class Dog extends Component {
        public render(): JSX.Element {
            return (
                <div className={this.props.breed}>
                    My {this.props.color} dog is {this.props.isGoodBoy ? "good" : "bad"}
                </div>
            )
        }
    }
    ```

    ```tsx
    /*Bad*/

    class Dog extends Component {
        public render(): JSX.Element {
            let breed = this.props.breed;
            let color = this.props.color;
            let isGoodBoy = this.props.isGoodBoy;

            return (
                <div className={breed}>
                    My {color} dog is {isGoodBoy ? "good" : "bad"}
                </div>
            )
        }
    }
    ```

    ```tsx
    /*Good*/

    class Dog extends Component {
        public render(): JSX.Element {
            let { breed, color, isGoodBoy } = this.props;

            return (
                <div className={breed}>
                    My {color} dog is {isGoodBoy ? "good" : "bad"}
                </div>
            )
        }
    }
    ```
* Put some coplex markups to functions or variables

    ```tsx
    /*Bad*/

    class Dog extends Component {
        public render(): JSX.Element {
            let { breed, color, isGoodBoy } = this.props;

            return (
                <div className={breed}>
                    My {color} dog is {isGoodBoy ? "good" : "bad"}
                </div>
            )
        }
    }
    ```

    ```tsx
    /*Good*/

    class Dog extends Component {
        public render(): JSX.Element {
            let { breed, color, isGoodBoy } = this.props;
            let identifier = isGoodBoy ? "good" : "bad";

            return (
                <div className={breed}>
                    My {color} dog is {identifier}
                </div>
            );
        }
    }
    ```

* Don't use `accesskey` for elements

    *Why?* The inconsistencies between the combination of keyboard shortcuts and keyboard commands make it difficult for people who use on-screen readers and keyboards.

    ```tsx
    /*Bad*/
    <div accessKey="h" />

    /*Good*/
    <div />
    ```

* Always add the `alt` attribute for `<img>` tags. If image is presentation then alt can be an empty string or `<img>` must have `role="presentation"`.

    ```tsx
    /*Bad*/
    <img src="hello.jpg" />

    /*Good*/
    <img src="hello.jpg" alt="Me waving hello" />

    /*Good*/
    <img src="hello.jpg" alt="" />

    /*Good*/
    <img src="hello.jpg" role="presentation" />
    ```

* Don't use index as `key` for elements. Prefer a unique ID. 

    *Why?* https://medium.com/@robinpokorny/index-as-a-key-is-an-anti-pattern-e0349aece318

    ```tsx
    /*Bad*/
    {todos.map((todo, index) =>
      <Todo
        {...todo}
        key={index}
      />
    )}

    /*Good*/
    {todos.map(todo => (
      <Todo
        {...todo}
        key={todo.id}
      />
    ))}
    ```

### Refs

* Always use callback function 

    ```tsx
    /*Bad*/
    <Foo
      ref="myRef"
    />

    /*Good*/
    <Foo
      ref={(ref) => { this.myRef = ref; }}
    />
    ```

### Tags

* Always use self closing tags if element doesn't have children

    ```tsx
    /*Bad*/
    <Foo variant="stuff"></Foo>

    /*Good*/
    <Foo variant="stuff" />
    ```

* If component have many attributes which are located on several lines, then close the tag on a new line.

    ```tsx
    /*Bad*/
    <Foo
      bar="bar"
      baz="baz" />

    /*Good*/
    <Foo
      bar="bar"
      baz="baz"
    />
    ```

### Methods

* Use arrow functions

    ```tsx
    class Listing extends React.Component {

      public log(name: string, index: number): void {
        /*Logic*/
      }

      public render(): JSX.Element {
        return (
          <ul>
            {props.items.map((item, index) => (
              <Item
                key={item.key}
                onClick={() => this.log(item.name, index)}
              />
            ))}
          </ul>
        );
      }
    }
    ```

## Redux

Libs `redux`, `react-redux` and `redux-observable`

* Use store structure by feature

    *Why?*: Easy to navigate and search

###
    src
    ├── store
        ├── auth
        ├── games
        ├── feature
            ├── index.ts
            ├── interfaces.ts/types.ts
            ├── feature.actions.ts
            ├── feature.effects.ts
            ├── feature.initial.ts
            ├── feature.reducer.ts
        ├── store.config.ts
        └── index.ts
    ├── ...

### Actions

* Use the follow codestyle. Action decorator will be in helper folder

```ts
import { Action } from 'redux';
import { action } from 'store/decorators';

export enum FeatureActionTypes {
  LoadData = '[feature] Load Data',
  LoadDataSuccess = '[feature] Load Data (Success)',
  LoadDataError = '[feature] Load Data (Error)',
}

@action()
export class LoadData implements Action {
  public readonly type = FeatureActionTypes.LoadData;

  constructor(public payload: string) { }
}

@action()
export class LoadDataSuccess implements Action {
  public readonly type = FeatureActionTypes.LoadDataSuccess;

  constructor(public payload: string) { }
}

@action()
export class LoadDataError implements Action {
  public readonly type = FeatureActionTypes.LoadDataError;
}

export type FeatureActions =
  | LoadData
  | LoadDataSuccess
  | LoadDataError;
```

### Effects

* Styles from `redux-observable`

```ts
export const loadData$ = (actions$:  ActionsObservable<JoinBattle>) =>
  actions$.ofType(FeatureActionTypes.LoadData).pipe(
    switchMap(({payload}) => service.loadData(payload).pipe(
      map(data => new LoadDataSuccess(data)),
      catchError(()=> of(new LoadDataError()))
    ),
  ),
);
```

### Reducer 

* Use `camelCase` for naming. 

     *Note*: Due to typescript and enum action types it makes possible to use intellisence.

```ts
import { FeatureActions, FeatureActionTypes } from './feature.action';
import { initialState } from './feature.initial';

export const featureReducer = (state = initialState, action: FeatureActions) => {
  switch (action.type) {

    case FeatureActionTypes.LoadDataSuccess: {
      return {
        ...state,
        status: Status.Loading
        data: action.payload
      };
    }

    case FeatureActionTypes.LoadDataSuccess: {
      return {
        ...state,
        status: Status.Success
        data: action.payload
      };
    }

    case FeatureActionTypes.LoadDataSuccess: {
      return {
        ...state,
        status: Status.Error
        data: undefined
      };
    }

    default:
      return state;
  }
};
```
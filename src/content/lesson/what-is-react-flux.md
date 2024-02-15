---
title: "Learn What is React Flux"
subtitle: "Without Flux, React is just a cute front-end library. React Flux will make it a framework, giving your application a defined structure, taking care of the data-processing layer, and more about flux."
cover_local: "../../assets/images/b84e07e5-5761-469b-85bb-f7afc87d4dc9.png"
textColor: "white"
date: "2020-10-19T16:36:31+00:00"
tags: ["reactjs","flux"]
status: "published"

---

> ### ⚠️Warning⚠️
> The following article has information that currently is deprecated by the React community. Instead is recommended the use of the hooks `useContext` and `useReducer` in combination to handle de app data, using native libraries, you can learn how to do this in [this article](https://4geeks.com/lesson/managin-react-app-data). The information presented in this article still may be useful for legacy systems that are currently running with this library, although is not recommended for new developments.

Remember how we always say that programming is like Taco Bell? It’s always the same ingredients, except differently! In this particular case, we are going to be relying heavily on Events to create our entire application architecture.

## Why do we need Flux?

We know you are still in the process of learning React. States and props can be confusing, and now, with Flux, things are going to get a little bit harder. But it’s for a good cause!

Without Flux, you can’t create medium or big React applications because everything will become disorganized pretty quickly.

Also, two different views are not able to send data between each other like the components do (using props) because all views are siblings and React Router is instantiating them. We need to have a common store shared between all the views that we are going to call "The Store."

Here is a list of all the advantages of using it:

+ It centralizes and **detaches the application data from the components:** database communication and data-processing will not depend anymore on how the application looks (renders).
+ It **controls the way your application data will flow:** it does not matter if the data was inputted by the user or coming from a database; everything will be available in a clear and accessible way.
+ It differentiates your components in **Views vs Re-usable components:** your components will remain being abstracted from your application logic, making them 100% reusable for future applications.

![React Flux](https://github.com/breatheco-de/content/blob/master/src/assets/images/aa1a5994-8de9-4d24-99ce-3a0d686c30bd.png?raw=true)

### Flux Divides the Application in 3 Layers:

|&nbsp;     |&nbsp;       |
|:-----------|:----------------|
Views (Components)     |Every React Component that calls any Flux action is called a view. The reason to call those components differently is that React components are supposed to communicate with each other through their props (without Flux).<br> <br>Once a React Component is hard-coded to Flux, you will not be able to reuse that component in the future (on this or any other development).       |
|Actions       |Actions can be triggered components (when the user clicks or interacts with the application) or by the system (for example, the auto-save functionality). Actions are the first step of any Flux workflow, and they always need to dispatch to the store.      |
|Store        |The store contains all the application data. It handles everything incoming from the dispatcher and determines the way data should be stored and retrieved.            |

## Building our first User History with Flux

The following project is a To-Do List application with 2 main user stories:

+ Create task (already developed and working).
+ Delete task.

To code the delete functionality, we have to update these files: (1) The Component (for when the user clicks on the track), (2) The Actions, (3) The Store (two times), and (4) The Component one last time. It's only 3 files and 5 updates. And you have to do that for every user story that you are going to build into your application.

> *In the end, working with Flux has to become something as automatic as riding a bike.*

![react flux](https://github.com/breatheco-de/content/blob/master/src/assets/images/77c93bfa-92cb-44e3-a7c5-c959e27c5ccc.jpeg?raw=true)

## Let's Implement the Delete Task Functionality

### 1) What user action starts the functionality?

(It’s always a typical JS event like click, hover, resize, etc.)

***Everything starts whenever the user clicks on the trash can icon. That is why we need to start our application by listening to the typical onClick event on the delete button.***

```javascript
// In the component that renders each to-do item we need to add a button and also an onClick listener that calls 
// the respective TodoAction.deleteTodo(task) function that we will create on the actions: 

<button onClick={()=>MyActions.deleteTodo(taskToDelete)}>delete</button>
```

### 2) Then we need to code our action inside the MyActions.js file like this:

```javascript
MyActions.js

// In this case, we decided that this function (a.k.a action) will receive the ID of the task to be deleted. 
class MyActions extends Flux.Actions{
    deleteTask(taskToDelete){
         // Get the current list of actions from the store 
        let currentActions = MyStore.getActions();
        let updatedActions = currentActions.filter((task) => {
             return (task.id != taskToDelete.id);
        });

        this.dispatch('MyStore.setActions', updatedActions);
    }
}
```

> ☝ This is a class component. We strongly recommend you to use functional components and hooks instead because class components are legacy.

### 3) Update the store to handle that new dispatched action

```javascript
// Inside the todoStore we have a HandleActions method that contains the logic to handle each dispatched action
// We have to add a new case to the switch with the name 'DELETE_TODO'  
// It has to match the name of the action that was dispatched
  
handleActions(action) {
  switch (action.type) {
    ...
    case 'DELETE_TODO': {
      this.deleteTodo(action.id);
      break;
    }
  }
}
```

### 4) Inside the To-Do Store, implement the actual logic for deleting the task and emitting the changes

```javascript

// Anywhere on your TodoStore class, add a new method that finally deletes the task from the todo list. 
// In this case we are using the filter function because it returns the same array but only with 
// the elements that match the logical question inside the filter (task.id != id) 

class TodoStore extends EventEmitter {
  ...
  deleteTodo(id){
    this.todos = this.todos.filter((task)=>{
       // Filter all tasks that have the given id 
      return (task.id != id);
    });
    this.emit('change');
  }
  ...
}
```

> ☝ This is a class component. We strongly recommend you to use functional components and hooks instead because class components are legacy.

## The Result

Finally, we have a new functionality implemented into our project. To keep adding more functionalities, you just have to start the Flux coding workflow from step 1 all over again.

<iframe src="https://codesandbox.io/embed/j1nvpono23" style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;" sandbox="allow-modals allow-forms allow-popups allow-scripts allow-same-origin"></iframe>

<div align="right"><small><a href="https://codesandbox.io/embed/j1nvpono23">Click here to open demo in a new window</a></small></div>




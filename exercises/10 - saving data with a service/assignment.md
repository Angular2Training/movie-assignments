Assignment 10: saving data with a service
==============================================

> ## Use the angular http service to save the movie details input to a remote/stub server

> The stub server we set up is also able to 'save' data by means of a http put (edit) or post (create) call.

**Links**:
- [http module](https://angular-2-training-book.rangle.io/handout/http/)
- [http request](https://angular-2-training-book.rangle.io/handout/http/making_requests.html)
- [convert to promise](https://angular-2-training-book.rangle.io/handout/http/requests_as_promises.html)
- [angular http client](https://angular.io/docs/ts/latest/guide/server-communication.html)
- [rxjs](http://reactivex.io/rxjs/manual/overview.html#introduction)
- [rxjs observable](http://reactivex.io/documentation/observable.html)
- [using observables](https://angular-2-training-book.rangle.io/handout/observables/using_observables.html)
- [promises](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [typescript generics](https://www.typescriptlang.org/docs/handbook/generics.html)
- [template literals](https://developers.google.com/web/updates/2015/01/ES6-Template-Strings)

**Steps**:
- Add an `updateMovie` function in the movie service, that receives one parameter `movie`.
- Create an local variable `url`, that combines the `moviesUrl` with a `/` and then the `movie.id`. So if `id` was one, the end result will be `api/movies/1`. *Tip: use a string template literal*.
- To send the data to the server, we need to convert the movie to a JSON string. Do this by calling `JSON.stringify(movie)`, and save the result in a variable `json`.
- call the `put` function on the `http` service, supply the url as first parameter and the `json` as second.
- Convert the observable result to a promise with `toPromise` and add the `then` function to the chain. Supply an arrow function as parameter to the `then` function which receives one parameter `response`. The value of the `response` parameter will be a http `204 No Content`, which means all went well, but the server did not send any data back. We don't want to send an empty response back to the movies component, so we will just return the `movie` object that was editted.
> Note: this means we must be able to rely on the server that the movie is stored exactly as we send it.
- To make it complete, also add the `catch` to the chain just like in `getMovies`.

> Now we want the data to be stored when we press a save button:
- Add a button element to the template of the details component, beneath the input fields. The button has the text `Save..` and a binding to it's `click` event. The `click` event is bound to a function `saveClicked`.
- Add the `saveClicked` function to the movie detail component.
> We want the movie detail component to remain stateless, i.e. not know anything about retreiving or saving data to a server, so we will let our parent handle the actual saving:
- Import the `Output` and `EventEmitter` from `@angular/core`, create an output property `save` and set its value to a new `EventEmitter`
- Call the `emit` function on `save` in the `saveClicked` method with the `movie` property as single argument.
- Add an event binding to the `save` event in the template of the movies component and bind it to `onSaveMovie`.
 - Add the `onSaveMovie` function to the movies detail component and call the `updateMovie` function of the movie service.
 - The `updateMovie` function will return a `Promise`, so chain the `then` function call and supply an arrow function as its single parameter.
 > Now that the data is saved, we want the list to update as well.
 - Extract the code from the `ngOnInit` function to a new function `getMovies` in the movies component and call the `getMovies` function in the `ngOnInit`. Now we can re-use the code we extracted (should not do that with the `ngOnInit`). 
- Now also call `getMovies` inside the arrow function after we saved.
 > Normally after editting a movie, we would return to a overview page or and retreive the updated list data.

**Result**:
> We now asynchronously save the data of an editted movie to a remote/stub server, and update the list after the data is saved.
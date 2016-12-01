Assignment 4: Creating a details component 
==============================================

## Create a new reusable component that shows the details of a movie and use it in the app component

- Create a new component in the `movie` folder using the angular-cli generator command `ng g component movie/movie-detail` in the integrated terminal;
  - Double check if the component is imported in the app module and added to the ngModule `declarations` array;
- Change the `selector` property of the movie-detail component to `movie-detail`;
- Import the angular `Input` decorator and create an input property `movie` of the type `Movie`;
- Copy the movie detail HTML from the app component template to the movie detail component template;
    - Make sure the property bindings (interpolation) are set to the movie property of the detail component;
- Replace the detail HTML in the app component template with the movie detail component;
  - Use the movie detail component by adding a `<movie-detail>` element;   
  - Add a property binding to the element that binds the input property `movie` to the `selectedMovie` of the app component;

The view will still show the details of the movie, but now via a reusable stateless component.

**Links**:
- [creating a component](https://angular-2-training-book.rangle.io/handout/components/creating_components.html)
- [input property binding](https://angular-2-training-book.rangle.io/handout/components/app_structure/passing_data_into_components.html)
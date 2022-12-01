#Testing

## 1.Check that passing a given input into our tests returns the expected output
    
## 2.Write tests to mimic the behaviour of a user performing different actions

## 3.Write testable, modular functions

## 4.Write functions that add, remove or modify DOM nodes


    const addToDoItem = (value, completed, taskId) => {
      const task = {
        title: value,
        completed: completed||false,
        id: taskId||new Date().getTime().toString(),
      }
      const li = document.createElement('li');
      li.innerHTML=task.title;
      li.setAttribute('id', task.id);
      li.setAttribute('data-completed', task.completed);
      toDoListDOM.prepend(li);
    };
    
    const toggleCompleted = (e) => {  
      const li = e.target.closest('li');
      const task = ToDoList.find((el) => el.id === li.getAttribute('id'));
      task.completed = !task.completed; //toggle
      li.dataset.completed = task.completed;
      const label = li.querySelector('label');
      if (task.completed === true) {
        toDoListDOMcompleted.prepend(li);
      } else {       
        toDoListDOM.prepend(li);
      }
    };

    
    const deleteTask(e) {
    if (e.target.tagName.toLowerCase() === 'button')
      {
        const li = e.target.closest('li');
        const id = li.getAttribute('id');
        const task = ToDoList.find(el => el.id === id);
        if (task.completed) {
          toDoListDOMcompleted.removeChild(li);
        } else {
          toDoListDOM.removeChild(li);
        }

        ToDoList.splice(ToDoList.findIndex(el => el.id === id), 1);
        updateLocalStorage(ToDoList);
      }
    } 
  
  

## 5.Apply event listeners to HTML form elements
    const form = document.querySelector('form');

   const submitHandler = (e) => {
      e.preventDefault();
      const nameEl = e.target.querySelector('#name');
      const ageEl = e.target.querySelector('#age');
      if (nameEl.value.trim() && ageEl.value.trim()) {
        addToDoItem(input.value.trim());
      } else {
        nameEl.classList.add('error');
        ageEl.classList.add('error');
      }
    };
    form.addEventListener('submit', submitHandler);
    
## 6.Use scope to control what variables are accessible inside functions and blocks
## 7.Use CSS grid to create complex layouts
## 8.Use CSS grid to make layouts that adapt to the viewport size

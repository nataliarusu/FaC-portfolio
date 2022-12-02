#Testing

## 1.Check that passing a given input into our tests returns the expected output

        test('addToDoItem("handle event listener") should add item to ToDoList array', ()=>{
            addToDoItem('add item to ToDoList');
            const task = ToDoList.find(el=>el.title==='add item to ToDoList');
            const actual= task? '[item in ToDoList]': '[item was\'t found in ToDoList]';
            const expected='[item in ToDoList]';
            equal(actual, expected); 
            toDoListDOM.removeChild(document.getElementById(task.id));
            ToDoList.splice(ToDoList.findIndex(el=>el.id===task.id), 1);
            updateLocalStorage(ToDoList);
         });
    
## 2.Write tests to mimic the behaviour of a user performing different actions

        test ('toggleCompleted() ev handler should toggle dataset.completed of li el',()=>{
            addToDoItem('test toggleCompleted function');
            const task = ToDoList.find(el=>el.title==='test toggleCompleted function');
            const input = document.getElementById(task.id).querySelector('input');
            input.click();
            console.log('clicked');
            let expected = 'data-completed = true';//from DOM
            let actual = `data-completed = ${input.closest('li').dataset.completed}`;
            equal(actual, expected);
            input.click();
            console.log('clicked');
            expected = 'data-completed = false';//from DOM
            actual = `data-completed = ${input.closest('li').dataset.completed}`;
            equal(actual, expected);
            toDoListDOM.removeChild(document.getElementById(task.id));
            ToDoList.splice(ToDoList.findIndex(el=>el.id===task.id), 1);
            updateLocalStorage(ToDoList);
        });

## 3.Write testable, modular functions
The code snippet below shows a function that returns an li element that can be tested


        const createLi = (newTask) => {
          const template = document.querySelector('template');
          const content = template.content.cloneNode(true);
          const li = content.querySelector('li');
          const span = li.querySelector('span');
          span.innerHTML = newTask.title;
          const input = li.querySelector('input[type="checkbox"]');
          input.addEventListener('change', toggleCompleted);
          li.setAttribute('id', newTask.id);
          li.setAttribute('data-completed', newTask.completed);
          return li;
        };

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

Scope in JavaScript refers to the current context of code, which determines the accessibility of variables to JavaScript. The two types of scope are local and global:
    
    - Global variables are those declared outside of a block
    - Local variables are those declared inside of a block
    
    
The code snippet below shows a function in which li, task and label variables are visible only inside the function because they are declared as const.<br>
The variable toDoListDOM is a global scoped variable therefore it is visible inside this function. 



        const toggleCompleted = (ev) => {  
          const li = ev.target.closest('li');
          const task = ToDoList.find((el) => el.id === li.getAttribute('id'));
          task.completed = !task.completed; //toggle
          li.dataset.completed = task.completed;
          const label = li.querySelector('label');
          if (task.completed === true) {
            label.append(addDone());
            toDoListDOMcompleted.prepend(li);
          } else {
            label.removeChild(label.querySelector('.done'));
            toDoListDOM.prepend(li);
          }
          updateLocalStorage(ToDoList);
        };

        
## 7.Use CSS grid to create complex layouts

        .history-list__container{
            background-color: white;
            box-shadow: 1px 2px 5px #c8d8d9;
            border-radius: 1px;
            margin: 1rem 0;
            min-height: 0;
            display: grid;
            grid-template-columns: 80% 20%;
        }
        .delete-container{
            grid-column-start: 2;
        }
        
## 8.Use CSS grid to make layouts that adapt to the viewport size

        .detaled__balance-display{
            max-width: 100%;    
            margin: auto;
            background-color: white;    
            padding: 20px;
            box-shadow: 1px 2px 5px #c8d8d9;
            display: grid;
            grid-template-columns: 100%;
            justify-content: center;
        }

        @media(min-width:450px){
            .detaled__balance-display{
                grid-template-columns: repeat(2, 50%);
                max-width: 50%;
            }
         }

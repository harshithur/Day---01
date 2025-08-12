# Day---01
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>To-Do List</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #1e1e2f;
      color: white;
      display: flex;
      justify-content: center;
      padding: 20px;
    }
    .container {
      background: #2a2a40;
      padding: 20px;
      border-radius: 10px;
      width: 350px;
    }
    h2 {
      margin-bottom: 10px;
    }
    input {
      width: 80%;
      padding: 8px;
      border-radius: 5px;
      border: none;
      background: #3a3a5a;
      color: white;
    }
    button.add {
      padding: 8px 12px;
      margin-left: 5px;
      border: none;
      background: #9b59b6;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }
    button.add:hover {
      background: #8e44ad;
    }
    .task {
      background: #3a3a5a;
      padding: 10px;
      border-radius: 5px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10px;
    }
    .task.done p {
      text-decoration: line-through;
      color: gray;
    }
    .task small {
      color: #bbb;
      font-size: 0.8em;
    }
    .actions button {
      background: none;
      border: none;
      color: white;
      cursor: pointer;
      font-size: 16px;
      margin-left: 5px;
    }
    .actions button:hover {
      color: #9b59b6;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Tasks - <span id="taskCount">0</span></h2>
    <div>
      <input type="text" id="taskInput" placeholder="Add a new task">
      <button class="add" onclick="addTask()">+</button>
    </div>
    <div id="taskList"></div>
  </div>

  <script>
    let tasks = [];

    function addTask() {
      const input = document.getElementById("taskInput");
      const text = input.value.trim();
      if (!text) return;
      
      const task = {
        id: Date.now(),
        text: text,
        done: false,
        date: new Date().toLocaleString()
      };
      tasks.push(task);
      input.value = "";
      renderTasks();
    }

    function toggleDone(id) {
      tasks = tasks.map(t => t.id === id ? {...t, done: !t.done} : t);
      renderTasks();
    }

    function deleteTask(id) {
      tasks = tasks.filter(t => t.id !== id);
      renderTasks();
    }

    function renderTasks() {
      const list = document.getElementById("taskList");
      list.innerHTML = "";
      tasks.forEach(task => {
        const div = document.createElement("div");
        div.className = "task" + (task.done ? " done" : "");
        div.innerHTML = `
          <div>
            <p>${task.text}</p>
            <small>${task.date}</small>
          </div>
          <div class="actions">
            <button onclick="toggleDone(${task.id})">✔</button>
            <button onclick="deleteTask(${task.id})">🗑</button>
          </div>
        `;
        list.appendChild(div);
      });
      document.getElementById("taskCount").textContent = tasks.length;
    }
  </script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>To-Do Web App</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    body {
      background-color: #1e1e2f;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 2rem;
      min-height: 100vh;
    }
    h1 {
      margin-bottom: 1rem;
      text-align: center;
      color: #4caf50;
      text-shadow: 0 0 10px rgba(76, 175, 80, 0.5);
    }
    .todo-container {
      background: #2c2c3e;
      padding: 2rem;
      border-radius: 1rem;
      width: 100%;
      max-width: 600px;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.4);
      transition: transform 0.3s;
    }
    .todo-container:hover {
      transform: translateY(-5px);
    }
    .todo-inputs {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }
    input, textarea, button, select {
      padding: 0.8rem;
      border: none;
      border-radius: 0.5rem;
      font-size: 1rem;
      transition: all 0.3s;
    }
    input:focus, textarea:focus, select:focus {
      outline: none;
      box-shadow: 0 0 0 2px #4caf50;
    }
    input[type="datetime-local"] {
      color: #000;
      background: white;
    }
    button {
      background: #4caf50;
      color: white;
      cursor: pointer;
      transition: all 0.3s;
      font-weight: bold;
    }
    button:hover {
      background: #45a049;
      transform: translateY(-2px);
    }
    button:active {
      transform: translateY(0);
    }
    .task-list {
      margin-top: 2rem;
      max-height: 400px;
      overflow-y: auto;
      padding-right: 10px;
    }
    .task-list::-webkit-scrollbar {
      width: 8px;
    }
    .task-list::-webkit-scrollbar-track {
      background: #2c2c3e;
    }
    .task-list::-webkit-scrollbar-thumb {
      background: #4caf50;
      border-radius: 4px;
    }
    .task-item {
      background: #3a3a5a;
      padding: 1rem;
      border-radius: 0.5rem;
      margin-bottom: 1rem;
      display: flex;
      flex-direction: column;
      transition: all 0.3s;
      position: relative;
      overflow: hidden;
    }
    .task-item:hover {
      transform: translateX(5px);
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    }
    .task-item.completed {
      background: #2e7d32;
      text-decoration: line-through;
      opacity: 0.8;
    }
    .task-item.completed::after {
      content: "✓";
      position: absolute;
      right: 10px;
      top: 10px;
      font-size: 24px;
      color: rgba(255, 255, 255, 0.3);
    }
    .task-actions {
      margin-top: 0.5rem;
      display: flex;
      gap: 0.5rem;
    }
    .task-actions button {
      flex: 1;
      background: #ff9800;
      padding: 0.5rem;
    }
    .task-actions button.complete {
      background: #2196f3;
    }
    .task-actions button.delete {
      background: #f44336;
    }
    .task-priority {
      position: absolute;
      right: 10px;
      top: 10px;
      width: 10px;
      height: 10px;
      border-radius: 50%;
    }
    .priority-high {
      background: #f44336;
      box-shadow: 0 0 10px #f44336;
    }
    .priority-medium {
      background: #ff9800;
      box-shadow: 0 0 10px #ff9800;
    }
    .priority-low {
      background: #4caf50;
      box-shadow: 0 0 10px #4caf50;
    }
    .stats {
      display: flex;
      justify-content: space-between;
      margin-top: 1rem;
      padding: 1rem;
      background: #3a3a5a;
      border-radius: 0.5rem;
    }
    .stat-item {
      text-align: center;
    }
    .stat-value {
      font-size: 1.5rem;
      font-weight: bold;
      color: #4caf50;
    }
    .filter-controls {
      display: flex;
      gap: 0.5rem;
      margin-top: 1rem;
    }
    .filter-controls button {
      flex: 1;
      background: #3a3a5a;
    }
    .filter-controls button.active {
      background: #4caf50;
    }
    .empty-state {
      text-align: center;
      padding: 2rem;
      color: #aaa;
    }
    .confetti {
      position: fixed;
      width: 10px;
      height: 10px;
      background-color: #f00;
      border-radius: 50%;
      animation: fall 5s linear forwards;
    }
    @keyframes fall {
      to {
        transform: translateY(100vh) rotate(360deg);
        opacity: 0;
      }
    }
    .category-tag {
      display: inline-block;
      padding: 0.2rem 0.5rem;
      border-radius: 1rem;
      font-size: 0.8rem;
      margin-top: 0.5rem;
      background: #4caf50;
    }
  </style>
</head>
<body>
  <h1>My Super To-Do App</h1>
  <div class="todo-container">
    <div class="todo-inputs">
      <input type="text" id="taskTitle" placeholder="Task title..." />
      <textarea id="taskDesc" placeholder="Task description..."></textarea>
      <input type="datetime-local" id="taskDateTime" />
      <select id="taskPriority">
        <option value="low">Low Priority</option>
        <option value="medium">Medium Priority</option>
        <option value="high">High Priority</option>
      </select>
      <input type="text" id="taskCategory" placeholder="Category (optional)" />
      <button onclick="addTask()">➕ Add Task</button>
    </div>

    <div class="filter-controls">
      <button class="active" onclick="filterTasks('all')">All Tasks</button>
      <button onclick="filterTasks('active')">Active</button>
      <button onclick="filterTasks('completed')">Completed</button>
    </div>

    <div class="stats">
      <div class="stat-item">
        <div class="stat-value" id="totalTasks">0</div>
        <div>Total</div>
      </div>
      <div class="stat-item">
        <div class="stat-value" id="activeTasks">0</div>
        <div>Active</div>
      </div>
      <div class="stat-item">
        <div class="stat-value" id="completedTasks">0</div>
        <div>Completed</div>
      </div>
    </div>

    <div class="task-list" id="taskList">
      <div class="empty-state">No tasks yet. Add your first task above!</div>
    </div>
  </div>

  <script>
    let tasks = [];
    let currentFilter = 'all';

    function addTask() {
      const title = document.getElementById("taskTitle").value;
      const desc = document.getElementById("taskDesc").value;
      const dateTime = document.getElementById("taskDateTime").value;
      const priority = document.getElementById("taskPriority").value;
      const category = document.getElementById("taskCategory").value;

      if (title.trim() === "") {
        alert("Please enter a task title.");
        return;
      }

      const task = {
        id: Date.now(),
        title,
        desc,
        dateTime,
        priority,
        category,
        completed: false,
        createdAt: new Date().toISOString()
      };

      tasks.push(task);
      renderTasks();
      clearInputs();
      updateStats();
      
      // Small animation for new task
      const taskList = document.getElementById("taskList");
      if (taskList.children.length > 0) {
        const lastTask = taskList.lastChild;
        lastTask.style.transform = "scale(0.9)";
        lastTask.style.opacity = "0";
        setTimeout(() => {
          lastTask.style.transform = "scale(1)";
          lastTask.style.opacity = "1";
        }, 10);
      }
    }

    function renderTasks() {
      const taskList = document.getElementById("taskList");
      taskList.innerHTML = "";

      const filteredTasks = tasks.filter(task => {
        if (currentFilter === 'active') return !task.completed;
        if (currentFilter === 'completed') return task.completed;
        return true;
      });

      if (filteredTasks.length === 0) {
        const emptyState = document.createElement("div");
        emptyState.className = "empty-state";
        emptyState.textContent = currentFilter === 'all' 
          ? "No tasks yet. Add your first task above!" 
          : `No ${currentFilter} tasks.`;
        taskList.appendChild(emptyState);
        return;
      }

      // Sort tasks: high priority first, then by date
      filteredTasks.sort((a, b) => {
        if (a.priority === 'high' && b.priority !== 'high') return -1;
        if (b.priority === 'high' && a.priority !== 'high') return 1;
        if (a.priority === 'medium' && b.priority === 'low') return -1;
        if (b.priority === 'medium' && a.priority === 'low') return 1;
        
        if (a.dateTime && b.dateTime) {
          return new Date(a.dateTime) - new Date(b.dateTime);
        }
        return 0;
      });

      filteredTasks.forEach((task) => {
        const taskDiv = document.createElement("div");
        taskDiv.className = `task-item ${task.completed ? "completed" : ""}`;
        
        const priorityClass = `priority-${task.priority}`;
        const priorityDot = `<div class="task-priority ${priorityClass}"></div>`;
        
        const categoryTag = task.category 
          ? `<span class="category-tag">${task.category}</span>` 
          : '';

        taskDiv.innerHTML = `
          ${priorityDot}
          <strong>${task.title}</strong>
          <p>${task.desc}</p>
          ${categoryTag}
          <small>📅 ${formatDateTime(task.dateTime)}</small>
          <div class="task-actions">
            <button class="complete" onclick="toggleComplete(${task.id})">
              ${task.completed ? "↩ Undo" : "✓ Complete"}
            </button>
            <button onclick="editTask(${task.id})">✏ Edit</button>
            <button class="delete" onclick="deleteTask(${task.id})">🗑 Delete</button>
          </div>
        `;

        taskList.appendChild(taskDiv);
      });
    }

    function formatDateTime(dateTimeString) {
      if (!dateTimeString) return "No deadline";
      
      const date = new Date(dateTimeString);
      return date.toLocaleString();
    }

    function toggleComplete(id) {
      const task = tasks.find(t => t.id === id);
      if (!task) return;
      
      task.completed = !task.completed;
      renderTasks();
      updateStats();
      
      if (task.completed) {
        createConfetti();
      }
    }

    function deleteTask(id) {
      tasks = tasks.filter((task) => task.id !== id);
      renderTasks();
      updateStats();
    }

    function editTask(id) {
      const task = tasks.find((t) => t.id === id);
      if (!task) return;

      document.getElementById("taskTitle").value = task.title;
      document.getElementById("taskDesc").value = task.desc;
      document.getElementById("taskDateTime").value = task.dateTime;
      document.getElementById("taskPriority").value = task.priority;
      document.getElementById("taskCategory").value = task.category || '';

      deleteTask(id);
      
      // Scroll to input form
      document.getElementById("taskTitle").focus();
    }

    function clearInputs() {
      document.getElementById("taskTitle").value = "";
      document.getElementById("taskDesc").value = "";
      document.getElementById("taskDateTime").value = "";
      document.getElementById("taskCategory").value = "";
      document.getElementById("taskPriority").value = "low";
    }

    function updateStats() {
      document.getElementById("totalTasks").textContent = tasks.length;
      document.getElementById("activeTasks").textContent = tasks.filter(t => !t.completed).length;
      document.getElementById("completedTasks").textContent = tasks.filter(t => t.completed).length;
    }

    function filterTasks(filter) {
      currentFilter = filter;
      renderTasks();
      
      // Update active button state
      document.querySelectorAll('.filter-controls button').forEach(btn => {
        btn.classList.toggle('active', btn.textContent.toLowerCase().includes(filter));
      });
    }

    function createConfetti() {
      const colors = ['#f44336', '#e91e63', '#9c27b0', '#673ab7', '#3f51b5', '#2196f3', '#03a9f4', '#00bcd4', '#009688', '#4CAF50', '#8BC34A', '#CDDC39', '#FFEB3B', '#FFC107', '#FF9800', '#FF5722'];
      
      for (let i = 0; i < 50; i++) {
        const confetti = document.createElement('div');
        confetti.className = 'confetti';
        confetti.style.left = `${Math.random() * 100}vw`;
        confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
        confetti.style.width = `${Math.random() * 10 + 5}px`;
        confetti.style.height = `${Math.random() * 10 + 5}px`;
        confetti.style.animationDuration = `${Math.random() * 3 + 2}s`;
        
        document.body.appendChild(confetti);
        
        setTimeout(() => {
          confetti.remove();
        }, 5000);
      }
    }

    // Initialize
    updateStats();
  </script>
</body>
</html>

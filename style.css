const form = document.getElementById("task-form");
const titleInput = document.getElementById("task-title");
const deadlineInput = document.getElementById("task-deadline");
const taskList = document.getElementById("task-list");
const emptyMessage = document.getElementById("empty-message");
const filterButtons = document.querySelectorAll(".filter-btn");

// Daftar tugas disimpan di variabel ini (hilang saat refresh)
let tasks = [];
let currentFilter = "all";

// Tambah tugas baru
form.addEventListener("submit", function (event) {
  event.preventDefault();

  const task = {
    id: Date.now(),
    title: titleInput.value.trim(),
    deadline: deadlineInput.value,
    done: false
  };

  tasks.push(task);
  form.reset();
  renderTasks();
});

// Ganti filter saat tombol diklik
filterButtons.forEach(function (button) {
  button.addEventListener("click", function () {
    currentFilter = button.dataset.filter;

    filterButtons.forEach(function (btn) {
      btn.classList.remove("active");
    });
    button.classList.add("active");

    renderTasks();
  });
});

// Tandai selesai / belum selesai
function toggleTask(id) {
  tasks = tasks.map(function (task) {
    if (task.id === id) {
      return { ...task, done: !task.done };
    }
    return task;
  });
  renderTasks();
}

// Hapus tugas
function deleteTask(id) {
  tasks = tasks.filter(function (task) {
    return task.id !== id;
  });
  renderTasks();
}

// Tampilkan daftar sesuai filter
function renderTasks() {
  taskList.innerHTML = "";

  const filtered = tasks.filter(function (task) {
    if (currentFilter === "pending") return !task.done;
    if (currentFilter === "done") return task.done;
    return true;
  });

  // Urutkan berdasarkan deadline terdekat
  filtered.sort(function (a, b) {
    return new Date(a.deadline) - new Date(b.deadline);
  });

  filtered.forEach(function (task) {
    const li = document.createElement("li");
    li.className = "task-item";

    const info = document.createElement("div");
    info.className = "task-info";

    const title = document.createElement("div");
    title.className = "task-title" + (task.done ? " done" : "");
    title.textContent = task.title;

    const deadline = document.createElement("div");
    deadline.className = "task-deadline";
    deadline.textContent = "Deadline: " + formatDate(task.deadline);

    info.appendChild(title);
    info.appendChild(deadline);

    const actions = document.createElement("div");
    actions.className = "task-actions";

    const toggleBtn = document.createElement("button");
    toggleBtn.className = "toggle-btn" + (task.done ? " undone" : "");
    toggleBtn.textContent = task.done ? "Batal" : "Selesai";
    toggleBtn.addEventListener("click", function () {
      toggleTask(task.id);
    });

    const deleteBtn = document.createElement("button");
    deleteBtn.className = "delete-btn";
    deleteBtn.textContent = "Hapus";
    deleteBtn.addEventListener("click", function () {
      deleteTask(task.id);
    });

    actions.appendChild(toggleBtn);
    actions.appendChild(deleteBtn);

    li.appendChild(info);
    li.appendChild(actions);
    taskList.appendChild(li);
  });

  emptyMessage.style.display = filtered.length === 0 ? "block" : "none";
}

// Ubah format tanggal jadi contoh: 15 Mar 2026
function formatDate(dateString) {
  const date = new Date(dateString);
  return date.toLocaleDateString("id-ID", {
    day: "numeric",
    month: "short",
    year: "numeric"
  });
}

renderTasks();
# Manajemen-Tugas <!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Pengelola Tugas Sekolah</title>
  <style>
    :root {
      --bg: #f1f5f9;
      --surface: #ffffff;
      --text: #0f172a;
      --text-muted: #64748b;
      --border: #e2e8f0;
      --primary: #2563eb;
      --primary-hover: #1d4ed8;
      --danger: #dc2626;
      --danger-bg: #fee2e2;
      --warning: #d97706;
      --warning-bg: #fef3c7;
      --success: #16a34a;
      --success-bg: #dcfce7;
      --info: #0284c7;
      --info-bg: #e0f2fe;
      --radius: 12px;
      --shadow: 0 4px 6px -1px rgb(0 0 0 / 0.07), 0 2px 4px -2px rgb(0 0 0 / 0.05);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
    }

    body {
      background-color: var(--bg);
      color: var(--text);
      line-height: 1.5;
      padding: 24px 16px;
    }

    .container {
      max-width: 1000px;
      margin: 0 auto;
    }

    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 12px;
      margin-bottom: 24px;
    }

    header h1 {
      font-size: 1.75rem;
      font-weight: 700;
      color: var(--text);
    }

    header p {
      color: var(--text-muted);
      font-size: 0.95rem;
    }

    /* Statistik Cards */
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      gap: 16px;
      margin-bottom: 24px;
    }

    .stat-card {
      background: var(--surface);
      padding: 16px 20px;
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      border-left: 4px solid var(--primary);
    }

    .stat-card.stat-pending { border-left-color: var(--warning); }
    .stat-card.stat-done { border-left-color: var(--success); }
    .stat-card.stat-urgent { border-left-color: var(--danger); }

    .stat-label {
      font-size: 0.85rem;
      color: var(--text-muted);
      font-weight: 600;
    }

    .stat-value {
      font-size: 1.75rem;
      font-weight: 700;
      margin-top: 4px;
    }

    /* Layout Form & List */
    .main-grid {
      display: grid;
      grid-template-columns: 340px 1fr;
      gap: 24px;
      align-items: start;
    }

    @media (max-width: 850px) {
      .main-grid {
        grid-template-columns: 1fr;
      }
    }

    .card {
      background: var(--surface);
      padding: 20px;
      border-radius: var(--radius);
      box-shadow: var(--shadow);
    }

    .card-title {
      font-size: 1.15rem;
      font-weight: 700;
      margin-bottom: 16px;
      padding-bottom: 10px;
      border-bottom: 1px solid var(--border);
    }

    /* Form */
    .form-group {
      margin-bottom: 14px;
    }

    label {
      display: block;
      font-size: 0.875rem;
      font-weight: 600;
      margin-bottom: 6px;
      color: var(--text);
    }

    input[type="text"],
    input[type="datetime-local"],
    select,
    textarea {
      width: 100%;
      padding: 10px 12px;
      border: 1px solid var(--border);
      border-radius: 8px;
      font-size: 0.95rem;
      background: #fff;
      color: var(--text);
      transition: border-color 0.2s;
    }

    input:focus, select:focus, textarea:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
    }

    textarea {
      resize: vertical;
      min-height: 70px;
    }

    .btn-group {
      display: flex;
      gap: 10px;
      margin-top: 16px;
    }

    button {
      cursor: pointer;
      border: none;
      border-radius: 8px;
      padding: 10px 16px;
      font-size: 0.95rem;
      font-weight: 600;
      transition: background 0.2s, transform 0.1s;
    }

    button:active {
      transform: scale(0.98);
    }

    .btn-primary {
      background: var(--primary);
      color: white;
      flex: 1;
    }

    .btn-primary:hover {
      background: var(--primary-hover);
    }

    .btn-secondary {
      background: var(--border);
      color: var(--text);
    }

    .btn-secondary:hover {
      background: #cbd5e1;
    }

    /* Filter Toolbar */
    .toolbar {
      display: grid;
      grid-template-columns: 1fr repeat(3, auto);
      gap: 10px;
      margin-bottom: 16px;
    }

    @media (max-width: 680px) {
      .toolbar {
        grid-template-columns: 1fr 1fr;
      }
      .toolbar input {
        grid-column: 1 / -1;
      }
    }

    /* Task List */
    .task-list {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .task-item {
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 16px;
      background: #fff;
      transition: box-shadow 0.2s;
      position: relative;
    }

    .task-item:hover {
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
    }

    .task-item.is-done {
      background: #f8fafc;
      opacity: 0.85;
    }

    .task-item.is-done .task-title {
      text-decoration: line-through;
      color: var(--text-muted);
    }

    .task-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      gap: 12px;
      margin-bottom: 8px;
    }

    .task-subject {
      font-size: 0.78rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.04em;
      color: var(--primary);
      margin-bottom: 4px;
    }

    .task-title {
      font-size: 1.08rem;
      font-weight: 700;
      word-break: break-word;
    }

    .task-desc {
      font-size: 0.9rem;
      color: var(--text-muted);
      margin-bottom: 12px;
      white-space: pre-line;
    }

    .badges {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      flex-shrink: 0;
    }

    .badge {
      padding: 4px 10px;
      border-radius: 999px;
      font-size: 0.78rem;
      font-weight: 700;
    }

    /* Priority Badges */
    .prio-tinggi { background: var(--danger-bg); color: var(--danger); }
    .prio-sedang { background: var(--warning-bg); color: var(--warning); }
    .prio-rendah { background: var(--info-bg); color: var(--info); }

    /* Deadline Indicator */
    .deadline-info {
      font-size: 0.85rem;
      display: flex;
      align-items: center;
      gap: 8px;
      flex-wrap: wrap;
    }

    .deadline-tag {
      font-weight: 700;
      padding: 2px 8px;
      border-radius: 6px;
      font-size: 0.78rem;
    }

    .dl-late { background: var(--danger-bg); color: var(--danger); }
    .dl-soon { background: var(--warning-bg); color: var(--warning); }
    .dl-normal { background: #f1f5f9; color: var(--text-muted); }
    .dl-done { background: var(--success-bg); color: var(--success); }

    .task-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 12px;
      margin-top: 12px;
      padding-top: 12px;
      border-top: 1px solid var(--border);
    }

    .status-select {
      width: auto;
      padding: 6px 10px;
      font-size: 0.85rem;
      font-weight: 600;
      border-radius: 6px;
    }

    .status-belum { background: #f1f5f9; color: #475569; }
    .status-proses { background: var(--warning-bg); color: var(--warning); }
    .status-selesai { background: var(--success-bg); color: var(--success); }

    .task-actions {
      display: flex;
      gap: 8px;
    }

    .btn-sm {
      padding: 6px 10px;
      font-size: 0.82rem;
    }

    .btn-edit {
      background: #e2e8f0;
      color: var(--text);
    }

    .btn-edit:hover { background: #cbd5e1; }

    .btn-delete {
      background: var(--danger-bg);
      color: var(--danger);
    }

    .btn-delete:hover { background: #fecaca; }

    .empty-state {
      text-align: center;
      padding: 40px 20px;
      color: var(--text-muted);
      border: 2px dashed var(--border);
      border-radius: 10px;
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div>
        <h1>Pengelola Tugas Sekolah</h1>
        <p>Catat deadline, pantau status pengerjaan, dan atur prioritas tugasmu.</p>
      </div>
    </header>

    <!-- Statistik -->
    <section class="stats-grid">
      <div class="stat-card">
        <div class="stat-label">Total Tugas</div>
        <div class="stat-value" id="statTotal">0</div>
      </div>
      <div class="stat-card stat-pending">
        <div class="stat-label">Belum Selesai</div>
        <div class="stat-value" id="statActive">0</div>
      </div>
      <div class="stat-card stat-done">
        <div class="stat-label">Sudah Selesai</div>
        <div class="stat-value" id="statDone">0</div>
      </div>
      <div class="stat-card stat-urgent">
        <div class="stat-label">Mendesak / Terlambat</div>
        <div class="stat-value" id="statUrgent">0</div>
      </div>
    </section>

    <div class="main-grid">
      <!-- Form Tambah / Edit Tugas -->
      <aside class="card">
        <h2 class="card-title" id="formTitle">Tambah Tugas Baru</h2>
        <form id="taskForm">
          <input type="hidden" id="taskId" />

          <div class="form-group">
            <label for="subject">Mata Pelajaran *</label>
            <input type="text" id="subject" placeholder="Contoh: Matematika, Biologi" required />
          </div>

          <div class="form-group">
            <label for="title">Nama Tugas *</label>
            <input type="text" id="title" placeholder="Contoh: Latihan Soal Bab 3" required />
          </div>

          <div class="form-group">
            <label for="deadline">Deadline *</label>
            <input type="datetime-local" id="deadline" required />
          </div>

          <div class="form-group">
            <label for="priority">Prioritas Tugas</label>
            <select id="priority">
              <option value="tinggi">Tinggi (Mendesak / Bobot Besar)</option>
              <option value="sedang" selected>Sedang</option>
              <option value="rendah">Rendah</option>
            </select>
          </div>

          <div class="form-group">
            <label for="status">Status Pengerjaan</label>
            <select id="status">
              <option value="belum">Belum Dikerjakan</option>
              <option value="proses">Sedang Dikerjakan</option>
              <option value="selesai">Selesai</option>
            </select>
          </div>

          <div class="form-group">
            <label for="notes">Catatan (Opsional)</label>
            <textarea id="notes" placeholder="Halaman buku, link materi, atau aturan pengumpulan..."></textarea>
          </div>

          <div class="btn-group">
            <button type="submit" class="btn-primary" id="submitBtn">Simpan Tugas</button>
            <button type="button" class="btn-secondary" id="cancelEditBtn" style="display: none;">Batal</button>
          </div>
        </form>
      </aside>

      <!-- Daftar Tugas -->
      <main class="card">
        <h2 class="card-title">Daftar Tugas</h2>

        <div class="toolbar">
          <input type="text" id="searchInput" placeholder="Cari tugas atau mata pelajaran..." />
          <select id="filterStatus" title="Filter Status">
            <option value="semua">Semua Status</option>
            <option value="belum">Belum Dikerjakan</option>
            <option value="proses">Sedang Dikerjakan</option>
            <option value="selesai">Selesai</option>
          </select>
          <select id="filterPriority" title="Filter Prioritas">
            <option value="semua">Semua Prioritas</option>
            <option value="tinggi">Prioritas Tinggi</option>
            <option value="sedang">Prioritas Sedang</option>
            <option value="rendah">Prioritas Rendah</option>
          </select>
          <select id="sortBy" title="Urutkan">
            <option value="deadline">Deadline Terdekat</option>
            <option value="priority">Prioritas Tertinggi</option>
            <option value="newest">Terbaru Ditambahkan</option>
          </select>
        </div>

        <div id="taskList" class="task-list"></div>
      </main>
    </div>
  </div>

  <script>
    const STORAGE_KEY = 'pengelola_tugas_sekolah_v1';

    // Elemen DOM
    const taskForm = document.getElementById('taskForm');
    const taskIdInput = document.getElementById('taskId');
    const subjectInput = document.getElementById('subject');
    const titleInput = document.getElementById('title');
    const deadlineInput = document.getElementById('deadline');
    const priorityInput = document.getElementById('priority');
    const statusInput = document.getElementById('status');
    const notesInput = document.getElementById('notes');

    const formTitle = document.getElementById('formTitle');
    const submitBtn = document.getElementById('submitBtn');
    const cancelEditBtn = document.getElementById('cancelEditBtn');

    const searchInput = document.getElementById('searchInput');
    const filterStatus = document.getElementById('filterStatus');
    const filterPriority = document.getElementById('filterPriority');
    const sortBy = document.getElementById('sortBy');
    const taskListEl = document.getElementById('taskList');

    // Data tugas
    let tasks = loadTasks();

    function loadTasks() {
      const saved = localStorage.getItem(STORAGE_KEY);
      if (saved) {
        return JSON.parse(saved);
      }
      // Contoh data awal agar tampilan langsung terlihat
      const tomorrow = new Date(Date.now() + 86400000);
      tomorrow.setHours(23, 59, 0, 0);
      const nextWeek = new Date(Date.now() + 5 * 86400000);
      nextWeek.setHours(10, 0, 0, 0);

      const initialTasks = [
        {
          id: crypto.randomUUID ? crypto.randomUUID() : String(Date.now()),
          subject: 'Matematika',
          title: 'Tugas Persamaan Kuadrat (Halaman 45)',
          deadline: toLocalDateTimeInput(tomorrow),
          priority: 'tinggi',
          status: 'proses',
          notes: 'Kerjakan nomor 1 sampai 10 beserta caranya di buku tulis.',
          createdAt: Date.now()
        },
        {
          id: crypto.randomUUID ? crypto.randomUUID() : String(Date.now() + 1),
          subject: 'Bahasa Indonesia',
          title: 'Membuat Teks Laporan Hasil Observasi',
          deadline: toLocalDateTimeInput(nextWeek),
          priority: 'sedang',
          status: 'belum',
          notes: 'Dikumpulkan dalam format PDF.',
          createdAt: Date.now() - 1000
        }
      ];
      localStorage.setItem(STORAGE_KEY, JSON.stringify(initialTasks));
      return initialTasks;
    }

    function saveTasks() {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(tasks));
    }

    function toLocalDateTimeInput(date) {
      const pad = (n) => String(n).padStart(2, '0');
      return `${date.getFullYear()}-${pad(date.getMonth() + 1)}-${pad(date.getDate())}T${pad(date.getHours())}:${pad(date.getMinutes())}`;
    }

    function setDefaultDeadline() {
      if (!deadlineInput.value) {
        const d = new Date(Date.now() + 86400000);
        d.setHours(23, 59, 0, 0);
        deadlineInput.value = toLocalDateTimeInput(d);
      }
    }

    // Mencegah XSS saat render teks user
    function escapeHTML(str) {
      return str.replace(/[&<>"']/g, (m) => ({
        '&': '&amp;',
        '<': '&lt;',
        '>': '&gt;',
        '"': '&quot;',
        "'": '&#39;'
      }[m]));
    }

    function formatDeadline(deadlineStr) {
      const date = new Date(deadlineStr);
      return date.toLocaleString('id-ID', {
        weekday: 'short',
        day: 'numeric',
        month: 'short',
        year: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
      });
    }

    function getDeadlineStatus(deadlineStr, status) {
      if (status === 'selesai') {
        return { label: 'Selesai tepat waktu', className: 'dl-done', urgent: false };
      }

      const now = new Date();
      const dl = new Date(deadlineStr);
      const diffMs = dl - now;
      const diffHours = diffMs / (1000 * 60 * 60);
      const diffDays = Math.ceil(diffMs / (1000 * 60 * 60 * 24));

      if (diffMs < 0) {
        return { label: 'Terlambat!', className: 'dl-late', urgent: true };
      }
      if (diffHours <= 24) {
        return { label: `Kurang dari ${Math.max(1, Math.ceil(diffHours))} jam lagi`, className: 'dl-soon', urgent: true };
      }
      if (diffDays <= 2) {
        return { label: `${diffDays} hari lagi`, className: 'dl-soon', urgent: true };
      }
      return { label: `${diffDays} hari lagi`, className: 'dl-normal', urgent: false };
    }

    function updateStats() {
      const total = tasks.length;
      const done = tasks.filter(t => t.status === 'selesai').length;
      const active = total - done;
      const urgent = tasks.filter(t => t.status !== 'selesai' && getDeadlineStatus(t.deadline, t.status).urgent).length;

      document.getElementById('statTotal').textContent = total;
      document.getElementById('statActive').textContent = active;
      document.getElementById('statDone').textContent = done;
      document.getElementById('statUrgent').textContent = urgent;
    }

    function renderTasks() {
      updateStats();

      const query = searchInput.value.trim().toLowerCase();
      const fStatus = filterStatus.value;
      const fPrio = filterPriority.value;
      const sort = sortBy.value;

      let filtered = tasks.filter(task => {
        const matchQuery =
          task.title.toLowerCase().includes(query) ||
          task.subject.toLowerCase().includes(query) ||
          (task.notes && task.notes.toLowerCase().includes(query));
        const matchStatus = fStatus === 'semua' || task.status === fStatus;
        const matchPrio = fPrio === 'semua' || task.priority === fPrio;
        return matchQuery && matchStatus && matchPrio;
      });

      const prioRank = { tinggi: 3, sedang: 2, rendah: 1 };

      filtered.sort((a, b) => {
        // Selalu letakkan tugas yang sudah selesai di bawah jika sort berdasarkan deadline/prioritas
        if (sort !== 'newest' && (a.status === 'selesai') !== (b.status === 'selesai')) {
          return a.status === 'selesai' ? 1 : -1;
        }
        if (sort === 'deadline') {
          return new Date(a.deadline) - new Date(b.deadline);
        }
        if (sort === 'priority') {
          return prioRank[b.priority] - prioRank[a.priority] || new Date(a.deadline) - new Date(b.deadline);
        }
        return b.createdAt - a.createdAt;
      });

      if (filtered.length === 0) {
        taskListEl.innerHTML = `
          <div class="empty-state">
            <p><strong>Tidak ada tugas ditemukan.</strong></p>
            <p style="font-size: 0.9rem; margin-top: 4px;">Tambahkan tugas baru atau ubah filter pencarianmu.</p>
          </div>
        `;
        return;
      }

      const prioLabel = { tinggi: 'Prioritas Tinggi', sedang: 'Prioritas Sedang', rendah: 'Prioritas Rendah' };

      taskListEl.innerHTML = filtered.map(task => {
        const dlStatus = getDeadlineStatus(task.deadline, task.status);
        const isDoneClass = task.status === 'selesai' ? 'is-done' : '';

        return `
          <div class="task-item ${isDoneClass}">
            <div class="task-header">
              <div>
                <div class="task-subject">${escapeHTML(task.subject)}</div>
                <div class="task-title">${escapeHTML(task.title)}</div>
              </div>
              <div class="badges">
                <span class="badge prio-${task.priority}">${prioLabel[task.priority]}</span>
              </div>
            </div>

            ${task.notes ? `<div class="task-desc">${escapeHTML(task.notes)}</div>` : ''}

            <div class="deadline-info">
              <span><strong>Deadline:</strong> ${formatDeadline(task.deadline)}</span>
              <span class="deadline-tag ${dlStatus.className}">${dlStatus.label}</span>
            </div>

            <div class="task-footer">
              <select
                class="status-select status-${task.status}"
                onchange="changeStatus('${task.id}', this.value)"
                aria-label="Ubah status tugas"
              >
                <option value="belum" ${task.status === 'belum' ? 'selected' : ''}>Belum Dikerjakan</option>
                <option value="proses" ${task.status === 'proses' ? 'selected' : ''}>Sedang Dikerjakan</option>
                <option value="selesai" ${task.status === 'selesai' ? 'selected' : ''}>Selesai</option>
              </select>

              <div class="task-actions">
                <button class="btn-sm btn-edit" onclick="editTask('${task.id}')">Edit</button>
                <button class="btn-sm btn-delete" onclick="deleteTask('${task.id}')">Hapus</button>
              </div>
            </div>
          </div>
        `;
      }).join('');
    }

    // Tambah / Update Tugas
    taskForm.addEventListener('submit', (e) => {
      e.preventDefault();

      const id = taskIdInput.value;
      const taskData = {
        subject: subjectInput.value.trim(),
        title: titleInput.value.trim(),
        deadline: deadlineInput.value,
        priority: priorityInput.value,
        status: statusInput.value,
        notes: notesInput.value.trim()
      };

      if (id) {
        const index = tasks.findIndex(t => t.id === id);
        if (index !== -1) {
          tasks[index] = { ...tasks[index], ...taskData };
        }
        resetForm();
      } else {
        tasks.push({
          id: crypto.randomUUID ? crypto.randomUUID() : String(Date.now() + Math.random()),
          ...taskData,
          createdAt: Date.now()
        });
        taskForm.reset();
        setDefaultDeadline();
      }

      saveTasks();
      renderTasks();
    });

    function resetForm() {
      taskForm.reset();
      taskIdInput.value = '';
      formTitle.textContent = 'Tambah Tugas Baru';
      submitBtn.textContent = 'Simpan Tugas';
      cancelEditBtn.style.display = 'none';
      setDefaultDeadline();
    }

    cancelEditBtn.addEventListener('click', resetForm);

    // Fungsi global untuk aksi pada card tugas
    window.changeStatus = function(id, newStatus) {
      const task = tasks.find(t => t.id === id);
      if (task) {
        task.status = newStatus;
        saveTasks();
        renderTasks();
      }
    };

    window.editTask = function(id) {
      const task = tasks.find(t => t.id === id);
      if (!task) return;

      taskIdInput.value = task.id;
      subjectInput.value = task.subject;
      titleInput.value = task.title;
      deadlineInput.value = task.deadline;
      priorityInput.value = task.priority;
      statusInput.value = task.status;
      notesInput.value = task.notes || '';

      formTitle.textContent = 'Edit Tugas';
      submitBtn.textContent = 'Perbarui Tugas';
      cancelEditBtn.style.display = 'inline-block';

      window.scrollTo({ top: 0, behavior: 'smooth' });
    };

    window.deleteTask = function(id) {
      if (confirm('Yakin ingin menghapus tugas ini?')) {
        tasks = tasks.filter(t => t.id !== id);
        if (taskIdInput.value === id) {
          resetForm();
        }
        saveTasks();
        renderTasks();
      }
    };

    // Event listener untuk filter & pencarian
    searchInput.addEventListener('input', renderTasks);
    filterStatus.addEventListener('change', renderTasks);
    filterPriority.addEventListener('change', renderTasks);
    sortBy.addEventListener('change', renderTasks);

    // Inisialisasi awal
    setDefaultDeadline();
    renderTasks();
  </script>
</body>
</html>

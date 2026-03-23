<template>
  <div class="app-shell" :class="{ 'sidebar-collapsed': sidebarCollapsed }">

    <!-- Mobile backdrop -->
    <div
      class="sidebar-backdrop"
      :class="{ 'sidebar-backdrop--visible': sidebarOpen }"
      @click="sidebarOpen = false"
    />

    <!-- ── Sidebar ─────────────────────────────────── -->
    <aside class="sidebar" :class="{ 'sidebar--open': sidebarOpen }">

      <!-- Logo / Brand + Collapse toggle -->
      <div class="sidebar-header">
        <router-link to="/" class="sidebar-logo" @click="sidebarOpen = false">
          <span class="sidebar-logo-name">{{ t('nav.companyName') }}</span>
          <span class="sidebar-logo-sub">{{ t('nav.subtitle') }}</span>
        </router-link>
        <button
          class="sidebar-collapse-btn"
          @click="sidebarCollapsed = !sidebarCollapsed"
          :aria-label="sidebarCollapsed ? 'Expand sidebar' : 'Collapse sidebar'"
        >
          <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
            <path
              :d="sidebarCollapsed ? 'M6 3l5 5-5 5' : 'M10 3L5 8l5 5'"
              stroke="currentColor"
              stroke-width="1.75"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
        </button>
      </div>

      <!-- Primary Navigation -->
      <nav class="sidebar-nav">

        <router-link
          to="/"
          class="nav-item"
          exact-active-class="nav-item--active"
          :data-tooltip="t('nav.overview')"
          @click="sidebarOpen = false"
        >
          <svg class="nav-icon" viewBox="0 0 18 18" fill="none">
            <rect x="2" y="2" width="6" height="6" rx="1" stroke="currentColor" stroke-width="1.5"/>
            <rect x="10" y="2" width="6" height="6" rx="1" stroke="currentColor" stroke-width="1.5"/>
            <rect x="2" y="10" width="6" height="6" rx="1" stroke="currentColor" stroke-width="1.5"/>
            <rect x="10" y="10" width="6" height="6" rx="1" stroke="currentColor" stroke-width="1.5"/>
          </svg>
          <span class="nav-label">{{ t('nav.overview') }}</span>
        </router-link>

        <router-link
          to="/inventory"
          class="nav-item"
          active-class="nav-item--active"
          :data-tooltip="t('nav.inventory')"
          @click="sidebarOpen = false"
        >
          <svg class="nav-icon" viewBox="0 0 18 18" fill="none">
            <path d="M3 6l6-3 6 3v7l-6 3-6-3V6z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/>
            <path d="M9 3v12M3 6l6 3 6-3" stroke="currentColor" stroke-width="1.5"/>
          </svg>
          <span class="nav-label">{{ t('nav.inventory') }}</span>
        </router-link>

        <router-link
          to="/orders"
          class="nav-item"
          active-class="nav-item--active"
          :data-tooltip="t('nav.orders')"
          @click="sidebarOpen = false"
        >
          <svg class="nav-icon" viewBox="0 0 18 18" fill="none">
            <path d="M3 4h12M3 9h12M3 14h8" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span class="nav-label">{{ t('nav.orders') }}</span>
        </router-link>

        <router-link
          to="/spending"
          class="nav-item"
          active-class="nav-item--active"
          :data-tooltip="t('nav.finance')"
          @click="sidebarOpen = false"
        >
          <svg class="nav-icon" viewBox="0 0 18 18" fill="none">
            <circle cx="9" cy="9" r="7" stroke="currentColor" stroke-width="1.5"/>
            <path d="M9 5.5v7M7 7.5c0-.83.9-1.5 2-1.5s2 .67 2 1.5S10 10 9 10s-2 .67-2 1.5.9 1.5 2 1.5 2-.67 2-1.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span class="nav-label">{{ t('nav.finance') }}</span>
        </router-link>

        <router-link
          to="/demand"
          class="nav-item"
          active-class="nav-item--active"
          :data-tooltip="t('nav.demandForecast')"
          @click="sidebarOpen = false"
        >
          <svg class="nav-icon" viewBox="0 0 18 18" fill="none">
            <path d="M2 14l4-4 4 2 6-8" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M12 4h4v4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <span class="nav-label">{{ t('nav.demandForecast') }}</span>
        </router-link>

        <router-link
          to="/reports"
          class="nav-item"
          active-class="nav-item--active"
          data-tooltip="Reports"
          @click="sidebarOpen = false"
        >
          <svg class="nav-icon" viewBox="0 0 18 18" fill="none">
            <path d="M10 2H5a1 1 0 00-1 1v12a1 1 0 001 1h8a1 1 0 001-1V6l-4-4z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/>
            <path d="M10 2v4h4M6 10h6M6 13h4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span class="nav-label">Reports</span>
        </router-link>

        <router-link
          to="/backlog"
          class="nav-item"
          active-class="nav-item--active"
          data-tooltip="Backlog"
          @click="sidebarOpen = false"
        >
          <svg class="nav-icon" viewBox="0 0 18 18" fill="none">
            <circle cx="9" cy="9" r="7" stroke="currentColor" stroke-width="1.5"/>
            <path d="M9 5v4l2.5 2.5" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          </svg>
          <span class="nav-label">Backlog</span>
        </router-link>

      </nav>

      <!-- Utility Footer -->
      <div class="sidebar-footer">
        <LanguageSwitcher />
        <ProfileMenu
          @show-profile-details="showProfileDetails = true"
          @show-tasks="showTasks = true"
        />
      </div>

    </aside>
    <!-- ── End Sidebar ──────────────────────────────── -->

    <!-- ── Main Wrapper ─────────────────────────────── -->
    <div class="main-wrapper">

      <!-- Hamburger (mobile only) -->
      <button class="hamburger-btn" @click="sidebarOpen = true" aria-label="Open menu">
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none">
          <path d="M3 5h14M3 10h14M3 15h14" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
        </svg>
      </button>

      <FilterBar />

      <main class="main-content">
        <router-view />
      </main>

    </div>
    <!-- ── End Main Wrapper ──────────────────────────── -->

    <ProfileDetailsModal
      :is-open="showProfileDetails"
      @close="showProfileDetails = false"
    />

    <TasksModal
      :is-open="showTasks"
      :tasks="tasks"
      @close="showTasks = false"
      @add-task="addTask"
      @delete-task="deleteTask"
      @toggle-task="toggleTask"
    />

  </div>
</template>

<script>
import { ref, watch, onMounted, onUnmounted, computed } from 'vue'
import { useRouter } from 'vue-router'
import { api } from './api'
import { useAuth } from './composables/useAuth'
import { useI18n } from './composables/useI18n'
import FilterBar from './components/FilterBar.vue'
import ProfileMenu from './components/ProfileMenu.vue'
import ProfileDetailsModal from './components/ProfileDetailsModal.vue'
import TasksModal from './components/TasksModal.vue'
import LanguageSwitcher from './components/LanguageSwitcher.vue'

export default {
  name: 'App',
  components: {
    FilterBar,
    ProfileMenu,
    ProfileDetailsModal,
    TasksModal,
    LanguageSwitcher
  },
  setup() {
    const { currentUser } = useAuth()
    const { t } = useI18n()
    const router = useRouter()
    const showProfileDetails = ref(false)
    const showTasks = ref(false)
    const sidebarOpen = ref(false)
    const apiTasks = ref([])

    // Collapsed state: restore from localStorage, else auto-collapse on small desktops
    const storedCollapsed = localStorage.getItem('sidebar-collapsed')
    const sidebarCollapsed = ref(
      storedCollapsed !== null ? storedCollapsed === 'true' : window.innerWidth < 1280
    )

    // Persist preference on manual toggle
    watch(sidebarCollapsed, (val) => {
      localStorage.setItem('sidebar-collapsed', String(val))
    })

    // Auto-collapse / expand when the window crosses the 1280px breakpoint
    // only if the user has not set a manual preference in this session
    const mq = window.matchMedia('(max-width: 1279px)')
    const onMqChange = (e) => {
      if (storedCollapsed === null) {
        sidebarCollapsed.value = e.matches
      }
    }
    mq.addEventListener('change', onMqChange)
    onUnmounted(() => mq.removeEventListener('change', onMqChange))

    // Close mobile sidebar on route change
    router.afterEach(() => { sidebarOpen.value = false })

    // Merge mock tasks from currentUser with API tasks
    const tasks = computed(() => {
      return [...currentUser.value.tasks, ...apiTasks.value]
    })

    const loadTasks = async () => {
      try {
        apiTasks.value = await api.getTasks()
      } catch (err) {
        console.error('Failed to load tasks:', err)
      }
    }

    const addTask = async (taskData) => {
      try {
        const newTask = await api.createTask(taskData)
        apiTasks.value.unshift(newTask)
      } catch (err) {
        console.error('Failed to add task:', err)
      }
    }

    const deleteTask = async (taskId) => {
      try {
        const isMockTask = currentUser.value.tasks.some(t => t.id === taskId)
        if (isMockTask) {
          const index = currentUser.value.tasks.findIndex(t => t.id === taskId)
          if (index !== -1) {
            currentUser.value.tasks.splice(index, 1)
          }
        } else {
          await api.deleteTask(taskId)
          apiTasks.value = apiTasks.value.filter(t => t.id !== taskId)
        }
      } catch (err) {
        console.error('Failed to delete task:', err)
      }
    }

    const toggleTask = async (taskId) => {
      try {
        const mockTask = currentUser.value.tasks.find(t => t.id === taskId)
        if (mockTask) {
          mockTask.status = mockTask.status === 'pending' ? 'completed' : 'pending'
        } else {
          const updatedTask = await api.toggleTask(taskId)
          const index = apiTasks.value.findIndex(t => t.id === taskId)
          if (index !== -1) {
            apiTasks.value[index] = updatedTask
          }
        }
      } catch (err) {
        console.error('Failed to toggle task:', err)
      }
    }

    onMounted(loadTasks)

    return {
      t,
      showProfileDetails,
      showTasks,
      sidebarOpen,
      sidebarCollapsed,
      tasks,
      addTask,
      deleteTask,
      toggleTask
    }
  }
}
</script>

<style>
/* ── Reset ──────────────────────────────────────── */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  background: #f8fafc;
  color: #1e293b;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/* ── Design Tokens ──────────────────────────────── */
:root {
  --sidebar-width: 240px;
  --sidebar-collapsed-width: 64px;
  --sidebar-bg: #ffffff;
  --sidebar-border: #e2e8f0;
  --sidebar-z: 100;
  --nav-hover-bg: #f1f5f9;
  --nav-active-bg: #eff6ff;
  --nav-active-text: #2563eb;
  --nav-text: #475569;
  --nav-icon: #94a3b8;
  --main-bg: #f8fafc;
  --sidebar-font-size: 0.875rem;
  --sidebar-font-weight: 500;
  --logo-height: 64px;
}

/* ── App Shell ──────────────────────────────────── */
.app-shell {
  display: flex;
  min-height: 100vh;
}

/* ── Sidebar ────────────────────────────────────── */
.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  width: var(--sidebar-width);
  height: 100vh;
  background: var(--sidebar-bg);
  border-right: 1px solid var(--sidebar-border);
  z-index: var(--sidebar-z);
  display: flex;
  flex-direction: column;
  transition: width 0.22s ease;
  /* No overflow:hidden — allows footer dropdowns to escape */
}

.sidebar-header {
  height: var(--logo-height);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 0.875rem 0 1.25rem;
  border-bottom: 1px solid var(--sidebar-border);
  flex-shrink: 0;
  overflow: hidden; /* clips logo text during animation */
}

.sidebar-logo {
  text-decoration: none;
  display: flex;
  flex-direction: column;
  gap: 0.125rem;
  overflow: hidden;
  flex: 1;
  min-width: 0;
}

.sidebar-logo-name {
  font-size: 1rem;
  font-weight: 700;
  color: #0f172a;
  letter-spacing: -0.025em;
  line-height: 1.2;
  white-space: nowrap;
  opacity: 1;
  transition: opacity 0.15s ease;
}

.sidebar-logo-sub {
  font-size: 0.688rem;
  color: #64748b;
  font-weight: 400;
  line-height: 1.2;
  white-space: nowrap;
  opacity: 1;
  transition: opacity 0.15s ease;
}

/* ── Collapse toggle button ─────────────────────── */
.sidebar-collapse-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 1.75rem;
  height: 1.75rem;
  flex-shrink: 0;
  background: transparent;
  border: 1px solid transparent;
  border-radius: 0.375rem;
  cursor: pointer;
  color: #94a3b8;
  transition: background 0.15s ease, border-color 0.15s ease, color 0.15s ease;
}

.sidebar-collapse-btn:hover {
  background: var(--nav-hover-bg);
  border-color: var(--sidebar-border);
  color: #475569;
}

/* Nav section */
.sidebar-nav {
  flex: 1;
  overflow-y: auto;
  overflow-x: hidden;
  padding: 0.75rem;
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 0.625rem;
  padding: 0.5rem 0.75rem;
  border-radius: 0.375rem;
  font-size: var(--sidebar-font-size);
  font-weight: var(--sidebar-font-weight);
  color: var(--nav-text);
  text-decoration: none;
  transition: background 0.15s ease, color 0.15s ease, padding 0.22s ease, gap 0.22s ease;
  white-space: nowrap;
  position: relative; /* for tooltip pseudo-element */
}

.nav-item:hover {
  background: var(--nav-hover-bg);
  color: #0f172a;
}

.nav-item:hover .nav-icon {
  color: #475569;
}

.nav-item--active {
  background: var(--nav-active-bg);
  color: var(--nav-active-text);
}

.nav-item--active .nav-icon {
  color: var(--nav-active-text);
}

.nav-icon {
  width: 1.125rem;
  height: 1.125rem;
  color: var(--nav-icon);
  flex-shrink: 0;
  transition: color 0.15s ease;
}

.nav-label {
  flex: 1;
  overflow: hidden;
  text-overflow: ellipsis;
  opacity: 1;
  max-width: 200px;
  transition: opacity 0.15s ease, max-width 0.22s ease;
}

/* Sidebar footer */
.sidebar-footer {
  flex-shrink: 0;
  padding: 0.75rem;
  border-top: 1px solid var(--sidebar-border);
  display: flex;
  flex-direction: column;
  gap: 4px;
  position: relative;
  overflow: visible; /* allow dropdowns to open */
}

/* ── Main Wrapper ───────────────────────────────── */
.main-wrapper {
  flex: 1;
  margin-left: var(--sidebar-width);
  min-height: 100vh;
  background: var(--main-bg);
  display: flex;
  flex-direction: column;
  transition: margin-left 0.22s ease;
}

.main-content {
  flex: 1;
  padding: 1.5rem 2rem;
}

/* ── Collapsed sidebar state ────────────────────── */
.sidebar-collapsed .sidebar {
  width: var(--sidebar-collapsed-width);
}

.sidebar-collapsed .main-wrapper {
  margin-left: var(--sidebar-collapsed-width);
}

/* Header: center the toggle button when collapsed */
.sidebar-collapsed .sidebar-header {
  justify-content: center;
  padding: 0;
}

/* Fade out logo text */
.sidebar-collapsed .sidebar-logo-name,
.sidebar-collapsed .sidebar-logo-sub {
  opacity: 0;
}

.sidebar-collapsed .sidebar-logo {
  pointer-events: none;
  max-width: 0;
}

/* Nav items: center icon, hide label */
.sidebar-collapsed .sidebar-nav {
  padding: 0.75rem 0.5rem;
}

.sidebar-collapsed .nav-item {
  justify-content: center;
  padding: 0.625rem;
  gap: 0;
}

.sidebar-collapsed .nav-label {
  opacity: 0;
  max-width: 0;
  overflow: hidden;
}

/* Tooltip shown on hover in collapsed mode */
.sidebar-collapsed .nav-item::after {
  content: attr(data-tooltip);
  position: absolute;
  left: calc(100% + 10px);
  top: 50%;
  transform: translateY(-50%);
  background: #0f172a;
  color: #f8fafc;
  padding: 0.375rem 0.625rem;
  border-radius: 0.375rem;
  font-size: 0.75rem;
  font-weight: 500;
  white-space: nowrap;
  pointer-events: none;
  opacity: 0;
  z-index: 200;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  transition: opacity 0.12s ease;
}

.sidebar-collapsed .nav-item:hover::after {
  opacity: 1;
}

/* Footer: center icons, hide text labels */
.sidebar-collapsed .sidebar-footer {
  padding: 0.5rem;
  align-items: center;
}

.sidebar-collapsed .sidebar-footer .profile-button,
.sidebar-collapsed .sidebar-footer .language-button {
  justify-content: center;
  padding: 0.625rem;
}

.sidebar-collapsed .sidebar-footer .profile-name,
.sidebar-collapsed .sidebar-footer .chevron,
.sidebar-collapsed .sidebar-footer .chevron-open,
.sidebar-collapsed .sidebar-footer .language-label {
  display: none;
}

/* In collapsed mode: footer dropdowns open to the right */
.sidebar-collapsed .sidebar-footer .profile-menu .dropdown-menu,
.sidebar-collapsed .sidebar-footer .language-switcher .dropdown-menu {
  bottom: 0;
  left: calc(100% + 8px);
}

/* ── Hamburger (mobile only) ────────────────────── */
.hamburger-btn {
  display: none;
}

/* ── Mobile sidebar backdrop ────────────────────── */
.sidebar-backdrop {
  display: none;
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.4);
  z-index: 99;
}

.sidebar-backdrop--visible {
  display: block;
}

/* ── Mobile responsive ──────────────────────────── */
@media (max-width: 767px) {
  .sidebar {
    transform: translateX(-100%);
    transition: transform 0.25s ease, width 0.22s ease;
    /* On mobile always use full width so all nav labels show */
    width: var(--sidebar-width) !important;
  }

  .sidebar--open {
    transform: translateX(0);
  }

  .main-wrapper,
  .sidebar-collapsed .main-wrapper {
    margin-left: 0;
  }

  /* Restore all collapsed-state overrides for mobile */
  .sidebar-collapsed .sidebar-logo {
    pointer-events: auto;
    max-width: 200px;
  }

  .sidebar-collapsed .sidebar-logo-name,
  .sidebar-collapsed .sidebar-logo-sub {
    opacity: 1;
  }

  .sidebar-collapsed .sidebar-header {
    justify-content: space-between;
    padding: 0 0.875rem 0 1.25rem;
  }

  .sidebar-collapsed .nav-item {
    justify-content: flex-start;
    padding: 0.5rem 0.75rem;
    gap: 0.625rem;
  }

  .sidebar-collapsed .nav-label {
    opacity: 1;
    max-width: 200px;
  }

  .sidebar-collapsed .sidebar-nav {
    padding: 0.75rem;
  }

  .sidebar-collapsed .sidebar-footer {
    padding: 0.75rem;
    align-items: stretch;
  }

  .sidebar-collapsed .sidebar-footer .profile-button,
  .sidebar-collapsed .sidebar-footer .language-button {
    justify-content: flex-start;
    padding: 0.5rem 0.75rem;
  }

  .sidebar-collapsed .sidebar-footer .profile-name,
  .sidebar-collapsed .sidebar-footer .chevron,
  .sidebar-collapsed .sidebar-footer .language-label {
    display: inline;
  }

  /* Hide tooltips on mobile (labels are always visible) */
  .sidebar-collapsed .nav-item::after {
    display: none;
  }

  /* Hide the desktop collapse button on mobile */
  .sidebar-collapse-btn {
    display: none;
  }

  .hamburger-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    position: fixed;
    top: 0.75rem;
    left: 0.75rem;
    z-index: 98;
    width: 2.25rem;
    height: 2.25rem;
    background: white;
    border: 1px solid #e2e8f0;
    border-radius: 0.375rem;
    cursor: pointer;
    color: #475569;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
  }

  .hamburger-btn:hover {
    background: #f8fafc;
    color: #0f172a;
  }

  .main-content {
    padding: 1rem;
  }
}

/* ── Global page structure ──────────────────────── */
.page-header {
  margin-bottom: 1.5rem;
}

.page-header h2 {
  font-size: 1.875rem;
  font-weight: 700;
  color: #0f172a;
  margin-bottom: 0.375rem;
  letter-spacing: -0.025em;
}

.page-header p {
  color: #64748b;
  font-size: 0.938rem;
}

/* ── Stats grid ─────────────────────────────────── */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.25rem;
  margin-bottom: 1.5rem;
}

.stat-card {
  background: white;
  padding: 1.25rem;
  border-radius: 10px;
  border: 1px solid #e2e8f0;
  transition: all 0.2s ease;
}

.stat-card:hover {
  border-color: #cbd5e1;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.06);
}

.stat-label {
  color: #64748b;
  font-size: 0.875rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 0.625rem;
}

.stat-value {
  font-size: 2.25rem;
  font-weight: 700;
  color: #0f172a;
  letter-spacing: -0.025em;
}

.stat-card.warning .stat-value { color: #ea580c; }
.stat-card.success .stat-value { color: #059669; }
.stat-card.danger  .stat-value { color: #dc2626; }
.stat-card.info    .stat-value { color: #2563eb; }

/* ── Card ───────────────────────────────────────── */
.card {
  background: white;
  border-radius: 10px;
  padding: 1.25rem;
  border: 1px solid #e2e8f0;
  margin-bottom: 1.25rem;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  padding-bottom: 0.875rem;
  border-bottom: 1px solid #e2e8f0;
}

.card-title {
  font-size: 1.125rem;
  font-weight: 700;
  color: #0f172a;
  letter-spacing: -0.025em;
}

/* ── Table ──────────────────────────────────────── */
.table-container {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}

thead {
  background: #f8fafc;
  border-top: 1px solid #e2e8f0;
  border-bottom: 1px solid #e2e8f0;
}

th {
  text-align: left;
  padding: 0.5rem 0.75rem;
  font-weight: 600;
  color: #475569;
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

td {
  padding: 0.5rem 0.75rem;
  border-top: 1px solid #f1f5f9;
  color: #334155;
  font-size: 0.875rem;
}

tbody tr {
  transition: background-color 0.15s ease;
}

tbody tr:hover {
  background: #f8fafc;
}

/* ── Badges ─────────────────────────────────────── */
.badge {
  display: inline-block;
  padding: 0.313rem 0.75rem;
  border-radius: 6px;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.025em;
}

.badge.success    { background: #d1fae5; color: #065f46; }
.badge.warning    { background: #fed7aa; color: #92400e; }
.badge.danger     { background: #fecaca; color: #991b1b; }
.badge.info       { background: #dbeafe; color: #1e40af; }
.badge.increasing { background: #d1fae5; color: #065f46; }
.badge.decreasing { background: #fecaca; color: #991b1b; }
.badge.stable     { background: #e0e7ff; color: #3730a3; }
.badge.high       { background: #fecaca; color: #991b1b; }
.badge.medium     { background: #fed7aa; color: #92400e; }
.badge.low        { background: #dbeafe; color: #1e40af; }

/* ── Sidebar footer component overrides ─────────── */
.sidebar-footer .profile-menu,
.sidebar-footer .language-switcher {
  width: 100%;
}

.sidebar-footer .profile-button,
.sidebar-footer .language-button {
  width: 100%;
  justify-content: flex-start;
  border-radius: 0.375rem;
  border-color: transparent;
  background: transparent;
  font-size: var(--sidebar-font-size);
  color: var(--nav-text);
  padding: 0.5rem 0.75rem;
  gap: 0.625rem;
}

.sidebar-footer .profile-button:hover,
.sidebar-footer .language-button:hover {
  background: var(--nav-hover-bg);
  border-color: transparent;
  color: #0f172a;
}

.sidebar-footer .profile-button .profile-name,
.sidebar-footer .language-button .language-label {
  font-size: var(--sidebar-font-size);
  font-weight: var(--sidebar-font-weight);
}

/* ── State helpers ──────────────────────────────── */
.loading {
  text-align: center;
  padding: 3rem;
  color: #64748b;
  font-size: 0.938rem;
}

.error {
  background: #fef2f2;
  border: 1px solid #fecaca;
  color: #991b1b;
  padding: 1rem;
  border-radius: 8px;
  margin: 1rem 0;
  font-size: 0.938rem;
}
</style>

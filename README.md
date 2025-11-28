# TaskFlow - React Todo App

A minimal React todo application showcasing hooks such as useState and useEffect along with common component patterns. This app is designed for WordPress developers familiar with jQuery, introducing the fundamentals of React and modern frontend development. It helps users understand the key similarities and differences between WordPress and React workflows.

## Features

- Add new todos
- Mark todos complete/incomplete
- Delete todos
- Filter: All / Active / Completed
- Clear all completed todos
- Persist to localStorage (survives browser refresh)
- Responsive design (mobile-friendly with CSS media queries)

---

## Part 1: Installing Prerequisites

Before setting up this project, you need Node.js (which includes npm). Think of Node.js as the "PHP" for JavaScript - it runs JavaScript code outside the browser.

### Install Node.js (includes npm)

**Windows:**
1. Go to https://nodejs.org/
2. Click the green **LTS** button (e.g., "18.x.x LTS Recommended For Most Users")
3. Download and run the `.msi` installer
4. Click **Next** through all steps (keep all defaults)
5. If asked about "Automatically install necessary tools", check the box
6. Click **Install**, then **Finish**
7. Open a **new** Command Prompt and verify:
   ```
   node -v
   npm -v
   ```
   Both commands should show version numbers.

**Mac:**

Option A - Direct download:
1. Go to https://nodejs.org/
2. Download the macOS installer (.pkg)
3. Run the installer

Option B - Using Homebrew:
```bash
brew install node
```

Verify:
```bash
node -v
npm -v
```

**Linux (Ubuntu/Debian):**
```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs

# Verify
node -v
npm -v
```

### Verify Prerequisites

```bash
node -v    # Should show v18.x.x or higher
npm -v     # Should show 9.x.x or higher
```

---

## Part 2: Setting Up TaskFlow

Unlike PHP projects, React projects are created using a command-line tool. We'll create a fresh React app, then replace the source files with our project files.

### Step 1: Create a New React App

Open Terminal (Mac/Linux) or Command Prompt (Windows):

```bash
# Navigate to your projects folder
cd ~/projects          # Mac/Linux
cd C:\projects         # Windows

# Create the React app (this takes 2-5 minutes)
npx create-react-app taskflow-react
```

**First time using npx?** Type `y` and press Enter when asked to install create-react-app.

Wait for the installation to complete. You'll see "Success! Created taskflow-react" when done.

### Step 2: Enter the Project Folder

```bash
cd taskflow-react
```

You should see files like `package.json`, `src/`, `public/`, etc.

### Step 3: Replace the Source Files

The default React app has demo content we don't need. Delete it and add our files:

**Delete existing src/ contents:**

Windows:
```
del src\*
```
(Type `Y` when asked to confirm)

Mac/Linux:
```bash
rm src/*
```

**Copy project files to src/:**

You need to copy these files from the downloaded project:
- `index.js` → `src/index.js`
- `App.js` → `src/App.js`
- `App.css` → `src/App.css`

Create the components folder and copy component files:

Windows:
```
mkdir src\components
```

Mac/Linux:
```bash
mkdir src/components
```

Then copy:
- `TodoList.js` → `src/components/TodoList.js`
- `TodoItem.js` → `src/components/TodoItem.js`
- `AddTodo.js` → `src/components/AddTodo.js`

### Step 4: Run the Application

```bash
npm start
```

Wait a few seconds for the first compilation. Your browser will automatically open to **http://localhost:3000** and you'll see the TaskFlow app!

**To stop the server:** Press `Ctrl + C` in Terminal.

---

## Component Structure

```
App
├── AddTodo        (Input form to add new todos)
└── TodoList       (Container for todo items)
    └── TodoItem   (Single todo with checkbox and delete)
```

Data flows down from App (which holds all state) to child components via props. Child components communicate back up using callback functions (onAdd, onToggle, onDelete).

---

## React Hooks Used

**useState** - Manages component state
```javascript
const [todos, setTodos] = useState([]);
```

**useEffect** - Syncs todos to localStorage
```javascript
useEffect(() => {
  localStorage.setItem('todos', JSON.stringify(todos));
}, [todos]);
```

---

## Project Structure

```
taskflow-react/
├── src/
│   ├── index.js              # Entry point
│   ├── App.js                # Main component (state lives here)
│   ├── App.css               # Styles
│   └── components/
│       ├── TodoList.js       # Maps todos to TodoItems
│       ├── TodoItem.js       # Single todo (checkbox, text, delete)
│       └── AddTodo.js        # Input form
├── public/                   # Static files (index.html)
├── netlify.toml              # Netlify deploy config
├── package.json              # Dependencies
└── README.md
```

---

## Key Lessons

React fundamentally changes how WordPress developers think about building UIs:

- **State vs DOM manipulation**: Instead of jQuery's `$('.element').hide()`, React re-renders components when state changes. You declare *what* the UI should look like, not *how* to change it.

- **Components vs template parts**: React components are like WordPress template parts but with built-in state management. Each component can have its own internal state.

- **Props vs global variables**: Data flows down through props, making it clear where data comes from. This is cleaner than WordPress's mix of global variables, template tags, and hooks.

- **localStorage vs database**: For simple apps, localStorage eliminates the need for a backend entirely. The browser stores data locally in JSON format.

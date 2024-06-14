# Vue 3 Todo App

This is a simple yet functional Todo application built using Vue 3, Vite, and Bootstrap. The app allows users to add, update, and delete tasks. Each task can be in one of three states: New, In Progress, or Completed, with the ability to change states accordingly.

## Features

- **Add New Todos:** Add tasks to your todo list.
- **Change Todo State:** Move tasks between New, In Progress, and Completed states.
- **Delete Todos:** Remove tasks from the list.
- **Double-Click Delete:** Double-click on a completed task to delete it.
- **State Colors:** Visual indication of task states using different colors.
- **Persistent Storage:** Tasks are saved in local storage and persist across page reloads.
- **Responsive Design:** Uses Bootstrap for a responsive and modern design.

## Demo

You can view the live demo of the application [here](https://your-username.github.io/vue-todo-app/).

## Installation

To run this project locally, follow these steps:

1. **Clone the repository:**

    ```bash
    git clone https://github.com/your-username/vue-todo-app.git
    cd vue-todo-app
    ```

2. **Install dependencies:**

    ```bash
    npm install
    ```

3. **Run the development server:**

    ```bash
    npm run dev
    ```

4. **Build for production:**

    ```bash
    npm run build
    ```

5. **Deploy to GitHub Pages:**

    ```bash
    npm run deploy
    ```

## Configuration

To configure the base URL for the GitHub Pages deployment, update the `base` property in `vite.config.js` to match your repository name:

```javascript
export default defineConfig({
  plugins: [vue()],
  base: '/vue-todo-app/' // Replace with your repo name
})

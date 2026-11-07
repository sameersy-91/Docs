# TaskFlow user guide

## Product overview

TaskFlow is a simple task management application. You use it to keep a list of tasks, mark tasks as complete, and remove tasks you no longer need.

TaskFlow runs as a local web service. It doesn't have a graphical interface. You work with tasks by sending requests to the service, either from a command-line tool such as `curl` or from your own application.

Use TaskFlow if you:

- Want a simple way to track tasks on your own computer.
- Are testing or learning how a task management API works.

> **Note:** TaskFlow stores tasks in memory only. When you stop the application, all tasks are deleted. TaskFlow doesn't include user accounts, so anyone who can reach the service can view and change its tasks.

## Before you begin

Make sure you have the following:

- **Python** installed on your computer. The application is written in Python.
- **pip**, the Python package installer. pip is included with most Python installations.
- **The TaskFlow files.** You need the `taskflow-demo` folder, which contains `app.py`, `requirements.txt`, and `README.md`.
- **A way to send web requests.** The examples in this guide use `curl`, which is included with Windows 10 and later, macOS, and most Linux distributions. You can also use any other HTTP client, such as Postman.

## Get started

1. Open a terminal and go to the `taskflow-demo` folder.

2. Install the required package:

   ```bash
   pip install -r requirements.txt
   ```

3. Start the application:

   ```bash
   python app.py
   ```

4. Keep the terminal window open. The application runs as long as the terminal is open.

5. To confirm that TaskFlow is running, list tasks. The service starts with an empty list, so the response is `[]`:

   ```bash
   curl http://127.0.0.1:5000/tasks
   ```

The service listens on `http://127.0.0.1:5000` by default. Use this address in all examples in this guide.

To stop TaskFlow, return to the terminal window and press **Ctrl+C**.

## Create a task

To create a task, send a request with a task title. You can also add an optional description.

1. Send a `POST` request to `/tasks`. Include a JSON body that contains a `title` value. To add a description, include a `description` value:

   ```bash
   curl -X POST http://127.0.0.1:5000/tasks \
     -H "Content-Type: application/json" \
     -d '{"title": "Buy milk", "description": "Two liters of whole milk"}'
   ```

2. Check the response. TaskFlow returns the new task with an ID, the title, the description, and a `completed` value set to `false`:

   ```json
   {
     "id": 1,
     "title": "Buy milk",
     "description": "Two liters of whole milk",
     "completed": false
   }
   ```

If you don't include a `description` value, TaskFlow saves the task with an empty description (`""`).

TaskFlow assigns each new task a unique ID. The ID increases by one for each task you create. You need the ID to complete or delete a task.

**Requirements for a title:**

- The request must include a `title` value.
- The title can't be empty.

If the title is missing or empty, TaskFlow returns an error. See [Troubleshooting](#troubleshooting).

## View tasks

To view all tasks, send a `GET` request to `/tasks`:

```bash
curl http://127.0.0.1:5000/tasks
```

TaskFlow returns a list of all tasks in the order you created them:

```json
[
  {
    "id": 1,
    "title": "Buy milk",
    "description": "Two liters of whole milk",
    "completed": false
  },
  {
    "id": 2,
    "title": "Write report",
    "description": "",
    "completed": true
  }
]
```

If you haven't created any tasks, or if you deleted all of them, TaskFlow returns an empty list: `[]`.

TaskFlow doesn't provide a way to view a single task, filter tasks, or sort tasks.

## Complete a task

To mark a task as complete, send a `PUT` request to `/tasks/<id>/complete`. Replace `<id>` with the ID of the task.

```bash
curl -X PUT http://127.0.0.1:5000/tasks/1/complete
```

TaskFlow returns the updated task, with `completed` set to `true`:

```json
{
  "id": 1,
  "title": "Buy milk",
  "description": "Two liters of whole milk",
  "completed": true
}
```

If you complete a task that is already complete, TaskFlow returns the task again. The task remains complete.

TaskFlow doesn't provide a way to mark a completed task as incomplete.

If no task has the ID you specify, TaskFlow returns an error. See [Troubleshooting](#troubleshooting).

## Delete a task

To delete a task, send a `DELETE` request to `/tasks/<id>`. Replace `<id>` with the ID of the task.

```bash
curl -X DELETE http://127.0.0.1:5000/tasks/1
```

If the task exists, TaskFlow deletes it and returns no content. The response is empty, with a status code of 204.

Deleted tasks can't be restored. TaskFlow doesn't assign a deleted task's ID to a new task.

If no task has the ID you specify, TaskFlow returns an error. See [Troubleshooting](#troubleshooting).

## Troubleshooting

The following errors are defined in the TaskFlow source code.

| Message | When it appears | What to do |
|---|---|---|
| `A task title is required.` (HTTP 400) | You create a task without a `title` value, or the `title` value is empty. | Include a non-empty `title` in the JSON body of your request. |
| `Task not found.` (HTTP 404) | You complete or delete a task, and no task has the ID you specified. | Run `GET /tasks` to view the current tasks and their IDs. Then use an ID from the list. Note that the ID is missing if you deleted the task or restarted TaskFlow. |

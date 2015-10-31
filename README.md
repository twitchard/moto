# MOTO
- Manual obstacle tracking oracle?
- Markdown-only task organizer?

Here are some ideas for how my ideal issue tracker would work.

## Goal 
The aim for moto is a task organizer (issue tracker) with minimal interface but maximal flexibility. 

### It's all about metadata
In a traditional task organizer, you control metadata (who is assigned, what is the priority, what is the status, who should be notified about updates, etc.) via clicking on menus and widgets. 

In moto, your task is a markdown document and metadata is specified inline using hashtags.

### Example
Here is an example task that specifies several different pieces of metadata:
``` make-moto.md
## Create an task organizer

We should write an task organizer in node.js. We should name it moto, after our little sister's stuffed lamb.

I've #assigned #twitchard and #atomopawn to do this, because they are 1337 hax0rz.

It's #priority 100, because existing task organizers are a crime against humanity which cause software engineers an inordinate amount of rage.

This task is #pending until Node Knockout begins.

That is #scheduled to happen at 2015-11-07 8:00 PM EST.

It only lasts 48 hours so it is #due on 2015-11-09 8:00 PM EST.

Since we aren't allowed to begin early, the task is about 0% #complete.
```

Rendered, that looks like
---
## Create an task organizer

We should write an task organizer in node.js. We should name it moto, after our little sister's stuffed lamb.

I've #assigned #twitchard and #atomopawn to do this, because they are 1337 hax0rz.

It's #priority 100, because existing task organizers are a crime against humanity which cause software engineers an inordinate amount of rage.

This task is #pending until Node Knockout begins.

That is #scheduled to happen at 2015-11-07 8:00 PM EST.

It only lasts 48 hours so it is #due on 2015-11-09 8:00 PM EST.

Since we aren't allowed to begin early, the task is about 0% #complete.

---



## Filtering
What if I am interesting in seeing all the tasks assigned to me? Then, I need only search for all the tasks with "#assigned" and "#twitchard" in the same line. Maybe I'm not interested in tasks that are finished, so I could exclude tasks that contain the hashtag "#done". Maybe I want to see all the highest priority tasks, then I display any tasks that contain the hashtag "#priority" followed by a number greater than 80.
Dates are tricky. For tasks due in the coming week, the logic is "display all tasks where the hashtag #due is on the same line as something that can be parsed and resolved to a date within the next week." Maybe we will have to enforce that dates follow a specific format, or maybe we can find an npm module to help parse natural language dates.

### Dashboards
Users should able to specify custom filters and save their filter as a "dashboard". Moto should also provide default dashboards for common use cases. 

#### Thumbnails
How does an issue appear on the dashboard? I think each issue gets a "slug" (the name of the document, like a filename), and a "short description" (the first line < 50 characters, like git?), but then possibly users will want to display various metadata on the thumbnail as well. (Who is assigned? What is the priority?) We should come up with a sensible default, but leave it customizable.

### Notifications
Users should be able to subscribe to receive an e-mail notification whenever a particular dashboard changes. For example, whenever a new issue is assigned to them, or when the status of an issue they are subscribed to changes. Maybe we should skip this for the hackathon, but we should definitely keep this in mind as we engineer the code.

## Web Interface
On the web interface you should be able to create/edit/view tasks, and display/save/view dashboards. I think we can skip access control for the hackathon.

## Command-line / File System Interface
I hate using my web browser, and I would love to update the progress of my issues in vim. Moto should provide a command-line utility that copies all the "tasks" of a project into a folder on the local machine, and opens up a socket to the main moto server to sync changes between the two. 

All the issues should live in the base directory.
Each dashboard should have a subdirectory with symbolic links to the issues in the main directory

For example
``` 
moto-client ./myProject 
```
might create a directory structure
```
./myProject
├── left-hand
|   ├── put-your-left-hand-in.md
|   └── put-your-left-hand-out.md
├── right-hand
|   ├── put-your-right-hand-in.md
|   └── put-your-right-hand-out.md
├── do-the-hokey-pokey.md
├── put-your-left-hand-in.md
├── put-your-left-hand-out.md
├── put-your-right-hand-in.md
├── put-your-right-hand-out.md
└── turn-yourself-about.md
```

# 📘 Training Format Selector — How to Update the Decision Tree

This document explains how to update the **HTML decision tool** used to recommend training formats.  
You can modify:

- Questions  
- Options  
- Results  
- Descriptions (with multi-line support)  
- Navigation logic  

All logic is stored inside a single JavaScript object called **`nodes`**.

---

## 🧱 1. Overview of the Structure

All decision logic is defined in the `<script>` section inside the HTML file.

Each **question node** looks like this:

```js
nodeId: {
  id: "nodeId",
  question: "Your question text",
  description: "Optional description text\nSupports multiple lines",
  options: [
    { label: "Button text", next: "otherNodeId" },
    { label: "Another choice", next: "anotherNode" }
  ]
}
```

Each **result node** looks like:

```js
nodeId: {
  id: "nodeId",
  result: "Final result text",
  description: "Explanation shown under the result\nSupports multiple lines"
}
```

---

## ✍️ 2. Adding a New Question

### Step 1 — Create a new node

```js
new_topic: {
  id: "new_topic",
  question: "Does this require hands-on learning?",
  description: "Use this question when the training involves practical exercises\nor technical steps.",
  options: [
    { label: "Yes", next: "hands_on_path" },
    { label: "No", next: "no_hands_on_path" }
  ]
}
```

### Step 2 — Link it from an existing node

```js
options: [
  { label: "New topic", next: "new_topic" }
]
```

---

## 🏁 3. Adding a New Result

### Step 1 — Create a result node

```js
advanced_result: {
  id: "advanced_result",
  result: "Advanced Training Module",
  description: "Use this for deep technical content or multi-step guided learning."
}
```

### Step 2 — Link a question to it

```js
options: [
  { label: "Go to advanced training", next: "advanced_result" }
]
```

---

## 📝 4. Adding or Updating Descriptions

Descriptions appear under:

- Questions  
- Results  

They support **multi-line text** using `\n`.

Example:

```js
description: "This is line 1\nThis is line 2\nThis is line 3"
```

The UI automatically converts `\n` into `<br>`.

---

## 🔗 5. Connecting Nodes Correctly

Every node must:

- Have a **unique `id`**
- Be connected using `next: "someNodeId"`
- Be referenced by at least one parent node (except `start`)

### Example flow:

```
start → audience → traceability → intro_elearning
```

---

## ⚠️ 6. Common Mistakes to Avoid

- Missing `next:` → buttons won’t work  
- Duplicate IDs → one node overwrites another  
- Missing commas → breaks the script  
- Missing descriptions → UI still works, but no text shows  

---

## 👨‍💻 7. Example — Adding a New Question and Result

```js
complexity_check: {
  id: "complexity_check",
  question: "Is the topic complex?",
  description: "Choose Yes for advanced subjects.\nChoose No for simpler content.",
  options: [
    { label: "Yes", next: "deep_training" },
    { label: "No", next: "quick_overview" }
  ]
},

deep_training: {
  id: "deep_training",
  result: "Deep Technical Training",
  description: "Used for hands-on, advanced training requiring detailed explanation."
},

quick_overview: {
  id: "quick_overview",
  result: "Quick Overview Video",
  description: "Short, simple content for fast onboarding."
}
```

---

## 📂 8. Where to Edit the File

Inside the HTML file, scroll down to the `nodes = { ... }` block:

```js
<script>
  const nodes = {
    ...
  }
</script>
```

All edits happen inside this object.

---

## 🎉 9. Finished!

To update the tool:

1. Add a new node  
2. Give it an `id`, `question`, or `result`  
3. Add a `description` (optional, supports `\n`)  
4. Connect it using `next:`  
5. Save and upload the file to SharePoint  

---

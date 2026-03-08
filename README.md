# Blog Application Models (Mongoose + TypeScript)

A simple **Blog App Models** built with **Node.js**, **TypeScript**, and **Mongoose**.
This project demonstrates a typical blog data model including **Users, Posts, Categories, and Comments**, with support for **nested comments and likes**.

---

## Features

* User system
* Blog post creation and management
* Categories and tags
* Nested comments (reply to comments)
* Like system for comments
* MongoDB indexing for better performance
* Clean schema design using Mongoose + TypeScript

---

## Tech Stack

* Node.js
* TypeScript
* MongoDB
* Mongoose
* Express.js

---

## Project Structure

### 1. MVC Structure
```
src
└── models
      ├── user.model.ts
      ├── post.model.ts
      ├── category.model.ts
      └── comment.model.ts
```

### 2. Feature/Module Structure

```
src
└── modules
    ├── category
    │   └── category.model.ts
    │
    ├── comment
    │   └── comment.model.ts
    │
    ├── post
    │   ├── post.constants.ts
    │   ├── post.model.ts
    │   └── post.types.ts
    │
    └── user
        └── user.model.ts
```

---

## Models

### User

Represents a user account.

Fields:

* `name` – Full name
* `email` – Unique email address
* `password` – Hashed password
* `avatar` – Profile image
* `role` – `user` or `admin`
* `createdAt`
* `updatedAt`

---

### Post

Represents a blog article.

Fields:

* `title` – Post title
* `slug` – SEO-friendly URL identifier
* `content` – Main post content
* `excerpt` – Short summary
* `author` – Reference to user
* `category` – Reference to category
* `tags` – Array of tags
* `featuredImage` – Cover image
* `likes` – Users who liked the post
* `published` – Publish status
* `publishedAt`
* `createdAt`
* `updatedAt`

---

### Category

Used to group posts.

Fields:

* `name`
* `slug`
* `description`
* `createdAt`
* `updatedAt`

---

### Comment

Represents comments on blog posts.

Fields:

* `post` – Reference to post
* `author` – Reference to user
* `content` – Comment text
* `likes` – Users who liked the comment
* `parentComment` – Reference for nested replies
* `createdAt`
* `updatedAt`

---

## Indexing Strategy

MongoDB indexes are used to improve query performance.

Examples:

```
postSchema.index({ slug: 1 }, { unique: true })
postSchema.index({ author: 1, createdAt: -1 })

commentSchema.index({ post: 1 })
commentSchema.index({ parentComment: 1 })
```

These indexes optimize:

* Post lookup by slug
* Fetching posts by author
* Loading comments for a post
* Loading nested replies

---

## Comment System

The comment system supports **threaded replies**.

Example structure:

```
Post
 └ Comment
     └ Reply
         └ Reply
```

This is implemented using the `parentComment` field.

---

## Like System

Posts and comments support likes.

Example:

```
likes: [ObjectId]
```

Each value represents a **user who liked the document**.

---


## Future Improvements

* Authentication (JWT)
* Pagination
* Search functionality
* Bookmark system
* Post view tracking
* Rate limiting

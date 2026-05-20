# 2.2 Asynchronous JavaScript

JavaScript is single-threaded, but we can handle asynchronous operations with callbacks, promises, and async/await.

## Callbacks

Pass a function to be called later.

### Basic Callback

```javascript
function fetchData(callback) {
  setTimeout(() => {
    const data = { id: 1, name: "John" };
    callback(data);
  }, 1000);
}

fetchData((data) => {
  console.log("Received:", data);
});
```

### Callback Hell (Avoid!)

```javascript
function getUser(id, callback) {
  setTimeout(() => callback({ id, name: "John" }), 1000);
}

function getPosts(userId, callback) {
  setTimeout(() => callback([{ id: 1, title: "Post 1" }]), 1000);
}

function getComments(postId, callback) {
  setTimeout(() => callback([{ id: 1, text: "Comment 1" }]), 1000);
}

// Callback Hell ❌
getUser(1, (user) => {
  getPosts(user.id, (posts) => {
    getComments(posts[0].id, (comments) => {
      console.log(user, posts, comments);
    });
  });
});
```

---

## Promises

Better way to handle async operations.

### Creating Promises

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Success!");
  }, 1000);
});

promise.then((result) => {
  console.log(result); // "Success!"
});
```

### Promise States

```javascript
// Pending → Fulfilled
const fulfilled = new Promise((resolve) => {
  resolve("Done");
});

// Pending → Rejected
const rejected = new Promise((resolve, reject) => {
  reject(new Error("Failed"));
});

fulfilled.then((result) => console.log(result));
rejected.catch((error) => console.log(error.message));
```

### Chain Promises

```javascript
fetch("/api/user/1")
  .then((response) => response.json())
  .then((user) => {
    console.log(user);
    return fetch(`/api/user/${user.id}/posts`);
  })
  .then((response) => response.json())
  .then((posts) => console.log(posts))
  .catch((error) => console.log("Error:", error));
```

### Promise Methods

```javascript
// Promise.all - All must succeed
Promise.all([
  fetch("/api/users"),
  fetch("/api/posts")
])
  .then(([usersRes, postsRes]) => {
    return Promise.all([usersRes.json(), postsRes.json()]);
  })
  .then(([users, posts]) => {
    console.log(users, posts);
  });

// Promise.race - First one wins
Promise.race([
  fetch("/api/data"),
  new Promise((_, reject) => 
    setTimeout(() => reject(new Error("Timeout")), 5000)
  )
]);
```

---

## Async/Await (Recommended)

Modern syntax for asynchronous code.

### Basic Async/Await

```javascript
async function getUser() {
  const response = await fetch("/api/user/1");
  const user = await response.json();
  return user;
}

getUser().then((user) => {
  console.log(user);
});

// Or in another async function
async function main() {
  const user = await getUser();
  console.log(user);
}

main();
```

### Error Handling

```javascript
async function fetchUser(id) {
  try {
    const response = await fetch(`/api/user/${id}`);
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }
    const user = await response.json();
    return user;
  } catch (error) {
    console.error("Error:", error.message);
    return null;
  } finally {
    console.log("Request completed");
  }
}
```

### Sequential vs Parallel

```javascript
// ❌ Sequential (slow)
async function slow() {
  const user = await fetch("/api/user/1").then(r => r.json());
  const posts = await fetch("/api/posts/1").then(r => r.json());
  return { user, posts };
  // Takes 2 seconds (1s + 1s)
}

// ✅ Parallel (fast)
async function fast() {
  const [user, posts] = await Promise.all([
    fetch("/api/user/1").then(r => r.json()),
    fetch("/api/posts/1").then(r => r.json())
  ]);
  return { user, posts };
  // Takes 1 second (both requests simultaneously)
}
```

---

## Real-World Example: API Integration

```javascript
async function searchUsers(query) {
  try {
    // Show loading state
    const loader = document.querySelector(".loader");
    loader.style.display = "block";
    
    // Fetch data
    const response = await fetch(
      `https://api.github.com/search/users?q=${query}`
    );
    
    if (!response.ok) {
      throw new Error("Search failed");
    }
    
    const data = await response.json();
    
    // Display results
    const results = document.querySelector(".results");
    results.innerHTML = data.items
      .map((user) => `
        <div class="user">
          <img src="${user.avatar_url}" />
          <h3>${user.login}</h3>
          <p>${user.html_url}</p>
        </div>
      `)
      .join("");
  } catch (error) {
    console.error("Error:", error);
    document.querySelector(".results").innerHTML = 
      `<p>Error: ${error.message}</p>`;
  } finally {
    // Hide loading
    document.querySelector(".loader").style.display = "none";
  }
}

// Use it
const input = document.querySelector("input");
input.addEventListener("input", (e) => {
  searchUsers(e.target.value);
});
```

---

## ✅ Practice Exercises

1. Fetch user data and display it
2. Fetch multiple resources in parallel
3. Implement retry logic with async/await
4. Handle timeout errors

---

## 🎯 Key Takeaways

✅ Avoid callback hell  
✅ Use promises or async/await  
✅ async/await is cleaner  
✅ Always handle errors  
✅ Use Promise.all for parallel requests  

---

**Next:** [03-error-handling.md](./03-error-handling.md)
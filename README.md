# @sfwnisme/visi

[![MIT License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![npm version](https://badge.fury.io/js/%40sfwnisme%2Fvisi.svg)](https://badge.fury.io/js/%40sfwnisme%2Fvisi)
[![TypeScript](https://img.shields.io/badge/TypeScript-Ready-blue.svg)](https://www.typescriptlang.org/)

`@sfwnisme/visi` is a React package that adapts SolidJS's powerful and efficient conditional rendering components. It offers a declarative API to conditionally render components based on given conditions, closely mimicking SolidJS's approach to reactive rendering in React.

This package aims to provide an efficient, easy-to-use, and flexible solution for handling conditional rendering in React applications, inspired by SolidJS's reactivity model.

## ✨ Features

- **Standardized Components:** Use only three components (Visible, Shift, Case) for all conditional rendering scenarios, simplifying code review and debugging.
- **Declarative Syntax:** Provides a clean and readable approach for handling conditions, avoiding complex inline logic.
- **Reusable Components:** Unify conditional rendering logic into reusable components for consistency across the application.
- **Callback Support:** Leverages the Function-as-Children Pattern to pass `when` prop value as the callback parameter, enhancing flexibility.
- **Simplified Nested Conditions:** Handles excessive nested conditions with clear and maintainable component structures.
- **Improved Readability:** Reduces clutter in deeply nested logic, making the code easier to understand.
- **Enhanced Bug Tracking:** Streamlines debugging by centralizing conditional logic into predictable patterns.
- **Switch Rendering Support:** Provides a robust alternative to switch or multiple if-else blocks using Shift and Case components.
- **Consistent Codebase:** Eliminates the need for varied snippets, promoting a uniform coding style.
- **React and SolidJS Inspiration**: Built to replicate SolidJS's efficient rendering while being tailored to React's ecosystem.

## 📦 Installation

Install the package using npm:

```bash
npm install @sfwnisme/visi
```

Or using yarn:

```bash
yarn add @sfwnisme/visi
```

## 🚀 Usage

### Single Render Comparison

#### 🟥 Traditional React

```tsx
// Approach 1
isAuthorized ? <Dashboard /> : <Login />

// Approach 2
if(!isAuthorized) {
  return <Login />
}
return <Dashboard />
```

#### 🟩 Visi

```tsx
// Single condition
<Visible when={isAuthorized} fallback={<Login />}>
  <Dashboard />
</Visible>

// Nested condition
<Visible when={isAuthorized} fallback={<Login />}>
  <Dashboard />
  <Visible when={isLogin}>
    <LogoutButton />
  </Visible>
</Visible>

// Callback condition
<Visible when={user} fallback={<p>loading...</p>}>
  {((userInfo: {name: string, age: string}) => (
    <p>{userInfo.name} is {userInfo.age} years old</p>
  ))}
</Visible>
```

### Shift Render Comparison

#### 🟥 Traditional React

```tsx
// Ternary approach
role === 'admin'
  ? <AdminDashboard />
  : role === 'supervisor'
    ? <SupervisorDashboard />
    : <UserDashboard />
  : <Login />;

// If-else approach
if(role === 'admin') {
  return <AdminDashboard />
}
if(role === 'supervisor') {
  return <SupervisorDashboard />
}
if(role === 'user') {
  return <UserDashboard />
}
return <Login />
```

#### 🟩 Visi

```tsx
<Shift fallback={<Login />}>
  <Case when={role === 'admin'}>
    <AdminDashboard />
  </Case>
  <Case when={role === 'supervisor'}>
    <SupervisorDashboard />
  </Case>
  <Case when={role === 'user'}>
    <UserDashboard />
  </Case>
</Shift>
```

### Excessive Complexity Render Comparison

#### 🟥 Traditional React

```tsx
<div>
  {user.role === 'admin' &&
    user.permissions.posts.view &&
    <Post>
      <h3>post conetent....</h3>
      {user.permissions.posts.comments.view &&
        <Comment>
          <div className="comment-box">
            <p>comment content...</p>
            {
              user.permissions.posts.comments.delete &&
              <Button>Delete</Button>
            }
            {
              user.permissions.posts.comments.update &&
              <Button>Update</Button>
            }
          </div>
          {user.permissions.posts.comments.reply.view &&
            <Replies>
              <Reply>
                <p>replay one content...</p>
                {
                  user.permissions.posts.comments.reply.delete &&
                  <Button>Delete</Button>
                }
                {
                  user.permissions.posts.comments.reply.update &&
                  <Button>Update</Button>
                }
              </Reply>
              {
                user.permissions.posts.comments.reply.create &&
                <CreateReply />
              }
            </Replies>
          }
        </Comment>
      }
    </Post>
  }
</div>
```

#### 🟩 Visi

```tsx
<Visible when={user.role === 'admin'}>
  <Visible when={user.permissions.posts.view}>
    <Post>
      <h3>post conetent....</h3>
      <Visible when={user.permissions.posts.comments.view}>
        <Comment>
          <div className="comment-box">
            <p>comment content...</p>
            <Visible when={user.permissions.posts.comments.delete}>
              <Button>Delete</Button>
            </Visible>
            <Visible when={user.permissions.posts.comments.update}>
              <Button>Update</Button>
            </Visible>
          </div>
          <Visible when={user.permissions.posts.comments.reply.view}>
            <Replies>
              <Reply>
                <p>replay one content...</p>
                <Visible when={user.permissions.posts.comments.reply.delete}>
                  <Button>Delete</Button>
                </Visible>
                <Visible when={user.permissions.posts.comments.reply.update}>
                  <Button>Update</Button>
                </Visible>
              </Reply>
              <Visible when={user.permissions.posts.comments.reply.create}>
                <CreateReply />
              </Visible>
            </Replies>
          </Visible>
        </Comment>
      </Visible>
    </Post>
  </Visible>
</Visible >
```

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📧 Contact

If you have any questions or suggestions, please open an issue on GitHub.

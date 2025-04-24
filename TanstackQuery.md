# TanStack Query (React Query) Cheat Sheet

## 1. Initialization

To start using TanStack Query, wrap your application with `QueryClientProvider`:

```tsx
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

const queryClient = new QueryClient();

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <YourComponent />
    </QueryClientProvider>
  );
}
```

---

## 2. Deduplication

TanStack Query automatically deduplicates requests — if the same queryKey is being used in multiple components at the same time, it will only fetch once and share the data.

```tsx
// Same queryKey = deduped request
useQuery({
  queryKey: ["users"],
  queryFn: fetchUsers,
});
```

---

## 3. Query Configuration with `staleTime`

```tsx
useQuery({
  queryKey: ["posts"],
  queryFn: fetchPosts,
  staleTime: 1000 * 60, // 1 minute
});
```

- `queryKey`: Unique identifier for the query.
- `queryFn`: Function to fetch the data.
- `staleTime`: Time (in ms) to consider data as "fresh". If data is fresh, it won't refetch on remount or focus.

---

## 4. `refetchInterval`

Automatically refetch data on an interval:

```tsx
useQuery({
  queryKey: ["notifications"],
  queryFn: fetchNotifications,
  refetchInterval: 10000, // every 10 seconds
});
```

---

## 5. Fetch from Multiple Endpoints

You can fetch multiple endpoints by combining them in a `queryFn`:

```tsx
useQuery({
  queryKey: ["dashboard"],
  queryFn: async () => {
    const [users, posts] = await Promise.all([
      fetch("/api/users").then((res) => res.json()),
      fetch("/api/posts").then((res) => res.json()),
    ]);
    return { users, posts };
  },
});
```

---

## 6. `useMutation` for Handling Mutations (Create, Update, Delete)

```tsx
import { useMutation } from "@tanstack/react-query";

const mutation = useMutation({
  mutationFn: async (newUser) => {
    const res = await fetch("/api/users", {
      method: "POST",
      body: JSON.stringify(newUser),
      headers: { "Content-Type": "application/json" },
    });
    if (!res.ok) throw new Error("Something went wrong");
    return res.json();
  },
  onSuccess: (data) => {
    console.log("User created successfully!", data);
  },
  onError: (error) => {
    console.error("Error:", error.message);
  },
});

// Trigger mutation
mutation.mutate({ name: "John", email: "john@example.com" });
```

---

## Explanation of Miscellaneous JavaScript Snippets

### `Promise.resolve(Math.random())`

This creates a Promise that immediately resolves to a random number between 0 and 1.

```js
Promise.resolve(Math.random()).then((value) => {
  console.log("Random value:", value);
});
```

Useful for simulating async values in mock tests.

---

### `JSON.stringify(data, null, 2)`

This converts a JavaScript object into a JSON string with pretty formatting (2-space indentation).

```js
const user = { name: "Imam", age: 20 };
console.log(JSON.stringify(user, null, 2));
```

Output:

```json
{
  "name": "Imam",
  "age": 20
}
```

Useful for debugging or displaying formatted JSON in UIs.

---

# Summary

This markdown covers:

- Basic setup and features of TanStack Query
- `useQuery` options like deduplication, staleTime, refetchInterval
- `useMutation` for handling POST, PUT, DELETE
- Explanation of some JavaScript expressions

For more advanced usage, visit the official docs: [TanStack Query Docs](https://tanstack.com/query/latest)

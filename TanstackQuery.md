### Tanstack Query:

1. **Initialization**

   - Install the required package:
     ```bash
     npm install @tanstack/react-query
     ```
   - Wrap your application with the `QueryClientProvider`:

     ```tsx
     import { QueryClient, QueryClientProvider } from "@tanstack/react-query";

     const queryClient = new QueryClient();

     function App() {
       return (
         <QueryClientProvider client={queryClient}>
           {/* Your application components */}
         </QueryClientProvider>
       );
     }
     ```

2. **Deduplication**

   - React Query automatically deduplicates requests with the same `queryKey` to avoid redundant network calls.

3. **State Time**

   - Configure the `staleTime` to define how long data is considered fresh:
     ```tsx
     useQuery({
       queryKey: ["data"],
       queryFn: fetchData,
       staleTime: 1000 * 60 * 5, // 5 minutes
     });
     ```

4. **Refetch Interval**

   - Automatically refetch data at a specified interval:
     ```tsx
     useQuery({
       queryKey: ["data"],
       queryFn: fetchData,
       refetchInterval: 1000 * 60, // 1 minute
     });
     ```

5. **Fetch From Multiple Endpoints**

   - Use multiple queries to fetch data from different endpoints:
     ```tsx
     const { data: data1 } = useQuery(["endpoint1"], fetchEndpoint1);
     const { data: data2 } = useQuery(["endpoint2"], fetchEndpoint2);
     ```

6. **useMutation**

   - Handle data mutations like create, update, or delete:

     ```tsx
     import { useMutation } from "@tanstack/react-query";

     const mutation = useMutation({
       mutationFn: updateData,
       onSuccess: () => {
         console.log("Data updated successfully");
       },
     });

     mutation.mutate({ id: 1, value: "newValue" });
     ```

### Additional Explanations:

- **`Promise.resolve(Math.random())`**

  - This creates a resolved promise with a random number as its value. Example:
    ```tsx
    Promise.resolve(Math.random()).then((value) => console.log(value));
    ```

- **`JSON.stringify(data, null, 2)`**
  - Converts a JavaScript object into a JSON string with indentation for readability. Example:
    ```tsx
    const data = { name: "John", age: 30 };
    console.log(JSON.stringify(data, null, 2));
    ```

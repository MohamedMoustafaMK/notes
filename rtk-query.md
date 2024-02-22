1. **Installation:**
   - Use a package manager to install the library. For example, if you're using npm for JavaScript, you might run: 
     ```
     npm install rtk-query
     ```

2. **Import the Library:**
   - In your code, import the library/module:
     ```javascript
     // For JavaScript/TypeScript
     import { createApi, fetchBaseQuery } from 'rtk-query';
     ```

3. **Configure API Client:**
   - Set up your API client by creating an instance with necessary configuration parameters:
     ```javascript
     const api = createApi({
       baseQuery: fetchBaseQuery({ baseUrl: 'https://api.example.com' }),
       endpoints: (builder) => ({
         // Define your API endpoints here
         getUsers: builder.query({
           query: () => 'users',  // Specify the endpoint path
         }),
       }),
     });
     ```

4. **Use API Endpoints:**
   - Utilize the created endpoints in your application:
     ```javascript
     // Call the getUsers endpoint
     const { data, error } = api.endpoints.getUsers.useQuery();

     if (error) {
       console.error('Error fetching users:', error);
     } else {
       console.log('Fetched users:', data);
     }
     ```

5. **Handle Authentication (if needed):**
   - If your API requires authentication, you might need to set up authentication headers or tokens. Refer to the library documentation for specifics.

6. **Handling Mutations:**
   - If your application involves data mutation (POST, PUT, DELETE), set up mutation endpoints and use them accordingly.

7. **Redux Toolkit Integration:**
   - Many modern API client libraries, including those built on Redux Toolkit (like rtk-query), integrate with Redux for state management. Make sure to set up your store and reducers as per the library documentation.

Remember to check the official documentation for the library you are using, as there may be specific features, configurations, or updates that are not covered in this generic guide.

## with axios

1. **Install Dependencies:**
   First, make sure you have both `rtk-query` and `axios` installed in your project.

   ```bash
   npm install rtk-query axios
   ```

2. **Configure API Client with Axios:**
   Create an API client configuration using Axios for the `baseQuery`.

   ```javascript
   // api.js (or wherever you configure your API)
   import { createApi, fetchBaseQuery } from 'rtk-query';
   import axios from 'axios';

   const api = createApi({
     baseQuery: fetchBaseQuery({
       baseUrl: 'https://api.example.com',
       // Configure Axios options here if needed
     }),
     endpoints: (builder) => ({
       getUsers: builder.query({
         query: () => 'users',
       }),
     }),
   });

   export const { useGetUsersQuery } = api;
   ```

3. **Use the API Endpoint in Your Component:**
   Now, you can use the generated query hook in your component:

   ```javascript
   // YourComponent.js
   import React, { useEffect } from 'react';
   import { useGetUsersQuery } from './api';  // Import the generated hook

   const YourComponent = () => {
     const { data, error, isLoading } = useGetUsersQuery();

     useEffect(() => {
       if (error) {
         console.error('Error fetching users:', error);
       }
     }, [error]);

     if (isLoading) {
       return <p>Loading...</p>;
     }

     return (
       <div>
         {data && (
           <ul>
             {data.map((user) => (
               <li key={user.id}>{user.name}</li>
             ))}
           </ul>
         )}
       </div>
     );
   };

   export default YourComponent;
   ```

Remember to handle loading states, errors, and other aspects according to your application's needs. This example assumes a basic understanding of React and assumes that you've set up your Redux store properly if `rtk-query` is using Redux Toolkit for state management. Adjust the code according to your project structure and requirements.
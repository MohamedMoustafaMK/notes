As of my last knowledge update in January 2022, I don't have specific information on an "rtk-query" library. However, I can provide you with a general guide on how to use a typical API client library in a programming language like JavaScript or Python. If "rtk-query" is a specific library or tool released after my last update, I recommend checking the official documentation for the most accurate and up-to-date information.

Here's a general guide on using an API client library:

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
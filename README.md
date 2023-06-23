# Multimedia-app

>This project builds a feature web app with React based on the base files from the campaign multimedia app from the stackup

## Why the feature was chosen
the reason I chose the `search` and `sort` features is because these two features are very helpful for tidying up a large number of files and when there are many files it will be easy to find the desired file with this features. I also edited to show the file type information and I added a date to make it more interesting.

## Added features
### _Search_
the code allows users to enter a search query in the input field. Whenever the user types or modifies the input, the `handleSearch` function is called, which updates the search query state and filters the `data` array based on the query. The filtered files are then displayed, and if the query is empty, all files are shown

#### How it works
At the first line the code initializes a state variable named `searchQuery` using the `useState` hook. It represents the current search query entered by the user. The second element returned by the `useState` hook is a function named `setSearchQuery`, used to update the value of the `searchQuery` state variable.

At the second line function `handleSearch` is called whenever the user performs a search.It takes a `query` parameter, which represents the user-entered search query.Inside the function, the `setSearchQuery` function is called to update the `searchQuery` state variable with the entered query.If the query is empty (i.e., the user cleared the search input), the code sets the `myFiles` state variable to the original data (`data`). This means all the files will be displayed again.The code filters the `data` array to find files that match the search query.The `filter` method is used on the `data` array, which takes a callback function that determines whether a file should be included in the filtered array or not.The callback function converts the file name and type to lowercase (for case-insensitive matching) and checks if either the file name or type includes the search query.The resulting filtered files are then set as the new value of the `myFiles `state variable.

At the third line search input code includes an input element of type "text" that serves as the search input field.The placeholder attribute provides a visual hint to the user, indicating that it is a search field.The `onChange` event handler is assigned to the input field. Whenever the user types or modifies the input, the event is triggered and the `handleSearch` function is called with the current value of the input (e.target.value).

```react code
// Define a state variable 'searchQuery' and a function 'setSearchQuery' to update it
const [searchQuery, setSearchQuery] = useState("");

// Function to handle the search operation
const handleSearch = (query) => {
  // Update the 'searchQuery' state with the entered query
  setSearchQuery(query);

  // If the query is empty, show all files by setting 'myFiles' to the original 'data'
  if (query === "") {
    setMyFiles(data);
    return;
  }

  // Filter the 'data' array to find files that match the search query
  const filteredFiles = data.filter((file) => {
    const fileName = file.name.toLowerCase();
    const fileType = file.type.toLowerCase();
    // Check if either the file name or type includes the search query (case-insensitive)
    return fileName.includes(query.toLowerCase()) || fileType.includes(query.toLowerCase());
  });

  // Set the filtered files as the new value of the 'myFiles' state
  setMyFiles(filteredFiles);
};

// Input field for the search functionality
<input
  type="text"
  placeholder="Search..."
  onChange={(e) => handleSearch(e.target.value)} // Call 'handleSearch' function whenever the input value changes
  style={styles.searchInput} // Apply the specified styles to the input field
/>
```

### _sort_
This code implements a sorting feature for a file list. Clicking the "Sort" button reveals two sort options: sorting by name and sorting by type. Selecting an option triggers the sorting logic, updates the file list, and hides the sort options.
#### How it works
At the first line the state variable `showSortOptions` is used to control the visibility of the sort options dropdown menu. When the "Sort" button is clicked, it toggles the value of `showSortOptions`, showing or hiding the sort options.

At the second line the `sortFiles` function takes an `option` parameter that represents the selected sorting option. It creates a copy of the `myFiles` array using the spread operator (`[...myFiles]`). This step is important to avoid directly modifying the original state. Depending on the selected option, the function sorts the `sortedFiles` array by either the `name` property or the `type` property using the `Array.sort` method and the `localeCompare` function for string comparison. Finally, it updates the state with the sorted array using the `setMyFiles` function.

At the third line the "Sort" button is rendered with an `onClick` event handler that toggles the visibility of the sort options dropdown  When this button is clicked, it toggles the visibility of the sort options by calling the `setShowSortOptions` function with the negation of the current value of `showSortOptions`.the next part, `{showSortOptions && (...)}`, is a conditional rendering. If `showSortOptions` is `true`, it renders the inner JSX code, which consists of a div container with the `styles.sortOptions` style applied. Inside this container, there are two `<button>` elements styled with `styles.sortOptionButton`. Each button represents a sorting option. When clicked, it calls the `sortFiles` function with the corresponding option ("name" or "type") and then hides the sort options by calling `setShowSortOptions(false)`.

```react code
// Indicates whether to show the sort options dropdown
const [showSortOptions, setShowSortOptions] = useState(false); 

// Function to sort files based on the selected option
  const sortFiles = (option) => {
    // Create a copy of the myFiles state array
    let sortedFiles = [...myFiles];
    // Perform sorting based on the selected option
    switch (option) {
      case "name":
        // Sort files by name in ascending order
        sortedFiles.sort((a, b) => a.name.localeCompare(b.name));  // Sort the files by name using localeCompare for string comparison
        break;
      case "type":
        // Sort files by type in ascending order
        sortedFiles.sort((a, b) => a.type.localeCompare(b.type)); // Sort the files by type using localeCompare for string comparison
        break;
      default:
        break;
    }
    // Update the myFiles state with the sorted files
    setMyFiles(sortedFiles); 
  };

// JSX code
<div style={styles.controlTools}>
              <button style={styles.controlButton}
                onClick={() => {
                  // Toggle the visibility of sort options when the button is clicked
                  setShowSortOptions(!showSortOptions); 
                }}
              > Sort </button>
              {showSortOptions && (
                <div style={styles.sortOptions}>
                  <button style={styles.sortOptionButton}
                    onClick={() => {
                      // Sort files by name and hide the sort options
                      sortFiles('name');
                      setShowSortOptions(false); 
                    }}
                  > Sort by name </button>
                  <button
                    style={styles.sortOptionButton}
                    onClick={() => {
                      // Sort files by type and hide the sort options
                      sortFiles('type'); 
                      setShowSortOptions(false); 
                    }}
                  > Sort by type </button>
                </div>
              )}
            </div>
```

## Thank You 
### End
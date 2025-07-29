sequenceDiagram
    participant browser
    participant server

    Note right of browser: User types a note and clicks "Save"

    browser->>browser: Prevent default form submission
    browser->>browser: Create note object with content and timestamp
    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/notes
        Note left of browser: Sends note data as JSON in request body
    activate server
    server-->>browser: Redirect response (302) to /exampleapp/notes
    deactivate server

    Note right of browser: Browser reloads the page due to redirect

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: the css file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: the JavaScript file
    deactivate server

    Note right of browser: JavaScript executes and fetches updated notes

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: Updated notes including the new one
    deactivate server

    Note right of browser: Callback function renders the updated notes

sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: JavaScript file for SPA
    deactivate server

    Note right of browser: JavaScript executes and fetches notes data

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: JSON data with notes
    deactivate server

    Note right of browser: Notes are rendered dynamically without page reload

sequenceDiagram
    participant browser
    participant server

    Note right of browser: User types a note and clicks "Save"

    browser->>browser: Create note object with content and timestamp
    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa
        Note left of browser: Sends note data as JSON
    activate server
    server-->>browser: Response with status (e.g. 201 Created)
    deactivate server

    Note right of browser: JavaScript updates the notes list dynamically
    browser->>browser: Append new note to DOM without reloading

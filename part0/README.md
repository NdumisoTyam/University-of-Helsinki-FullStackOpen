sequenceDiagram
    participant browser
    participant server

    browser->>server: GET /exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET /exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET /exampleapp/main.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    Note right of browser: JavaScript executes and fetches notes JSON

    browser->>server: GET /exampleapp/data.json
    activate server
    server-->>browser: Notes data (JSON)
    deactivate server

    Note right of browser: Callback renders the notes to the page

    sequenceDiagram
    participant browser
    participant server

    Note right of browser: User writes a note and clicks Save  
    Note right of browser: JavaScript intercepts form submission  
    Note right of browser: Payload is constructed with note content and date

    browser->>server: POST /exampleapp/new_note (form data)
    activate server
    server-->>browser: HTTP 302 Redirect to /exampleapp/notes
    deactivate server

    Note right of browser: Browser reloads the /notes page

    browser->>server: GET /exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET /exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET /exampleapp/main.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    Note right of browser: JavaScript fetches updated notes

    browser->>server: GET /exampleapp/data.json
    activate server
    server-->>browser: Updated notes data
    deactivate server

    Note right of browser: Callback renders updated notes list

    sequenceDiagram
    participant browser
    participant server

    browser->>server: GET /exampleapp/spa
    activate server
    server-->>browser: Minimal HTML document
    deactivate server

    browser->>server: GET /exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET /exampleapp/spa.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    Note right of browser: JavaScript fetches notes JSON

    browser->>server: GET /exampleapp/data.json
    activate server
    server-->>browser: Notes data (JSON)
    deactivate server

    Note right of browser: JavaScript dynamically renders notes

    sequenceDiagram
    participant browser
    participant server

    Note right of browser: User writes a note and clicks Save  
    Note right of browser: JavaScript creates note object with content and date

    browser->>server: POST /exampleapp/new_note_spa (JSON payload)
    activate server
    server-->>browser: HTTP 201 Created or confirmation
    deactivate server

    Note right of browser: JavaScript updates local notes list  
    Note right of browser: Page is updated without reload

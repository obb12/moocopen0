sequenceDiagram
    participant User
    participant browser
    participant server

    User->>browser: Enters note in text field
    User->>browser: Clicks "Save" button

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note (with payload: {"content": "user note", "date": "2023-1-1"})
    activate server
    server-->>browser: 200 OK (New note created)
    deactivate server

    Note right of browser: The browser continues running the SPA, no page reload

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, { "content": "user note", "date": "2023-1-1" }, ... ]
    deactivate server

    Note right of browser: The browser updates the list of notes dynamically without reloading the page

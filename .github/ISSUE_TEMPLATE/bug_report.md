---
name: Bug report
about: Create a report to help us improve
title: '// Gets a book. rpc GetBook(GetBookRequest) returns (Book) {   // Get maps
  to HTTP GET. Resource name is mapped to the URL. No body.   option (google.api.http)
  = {     // Note the URL template variable which captures the multi-segment resource     //
  name of the requested book, such as "shelves/shelf1/books/book2"     get: "/v1/{name=shelves/*/books/*}"   };
  }  message GetBookRequest {   // The field will contain name of the resource requested,
  for example:   // "shelves/shelf1/books/book2"   string name = 1; }'
labels: ''
assignees: ''

---

**Describe the bug**
A clear and concise description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Go to '...'
2. Click on '....'
3. Scroll down to '....'
4. See error

**Expected behavior**
A clear and concise description of what you expected to happen.

**Screenshots**
If applicable, add screenshots to help explain your problem.

**Desktop (please complete the following information):**
 - OS: [e.g. iOS]
 - Browser [e.g. chrome, safari]
 - Version [e.g. 22]

**Smartphone (please complete the following information):**
 - Device: [e.g. iPhone6]
 - OS: [e.g. iOS8.1]
 - Browser [e.g. stock browser, safari]
 - Version [e.g. 22]

**Additional context**
Add any other context about the problem here.

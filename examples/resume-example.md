# Resume

Objective: Add pagination to the /api/users endpoint
Next: Wire the cursor param into the SQL query in users_repo.go
Files:
- src/api/handlers/users.go
- src/db/users_repo.go
- src/api/handlers/users_test.go

Gotcha: The existing offset-based pagination must stay for v1 clients — add cursor as an alternative, don't replace
Start with: Open users_repo.go and add a CursorList method next to the existing List method

## Types of payloads received at API routes

---

## 1. JSON Body (most common)

```go
type CreateUserRequest struct {
    Name  string `json:"name"`
    Email string `json:"email"`
}

func createUser(w http.ResponseWriter, r *http.Request) {
    var req CreateUserRequest

    err := json.NewDecoder(r.Body).Decode(&req)
    if err != nil {
        http.Error(w, "invalid request body", http.StatusBadRequest)
        return
    }

    fmt.Println(req.Name, req.Email)
}
```

---

## 2. Query Parameters

```go
// URL: /users?page=1&limit=10

func getUsers(w http.ResponseWriter, r *http.Request) {
    page := r.URL.Query().Get("page")   // "1"
    limit := r.URL.Query().Get("limit") // "10"

    fmt.Println(page, limit)
}
```

---

## 3. Path Parameters

```go
// URL: /users/123

func getUser(w http.ResponseWriter, r *http.Request) {
    // using standard lib (Go 1.22+)
    id := r.PathValue("id")
    fmt.Println(id) // "123"
}

func main() {
    http.HandleFunc("/users/{id}", getUser)
}
```

---

## 4. Form Data

```go
// Content-Type: application/x-www-form-urlencoded

func handleForm(w http.ResponseWriter, r *http.Request) {
    r.ParseForm()

    name := r.FormValue("name")
    email := r.FormValue("email")

    fmt.Println(name, email)
}
```

---

## 5. Multipart Form (file uploads)

```go
// Content-Type: multipart/form-data

func handleFileUpload(w http.ResponseWriter, r *http.Request) {
    r.ParseMultipartForm(10 << 20) // 10MB limit

    file, handler, err := r.FormFile("upload")
    if err != nil {
        http.Error(w, "error retrieving file", http.StatusBadRequest)
        return
    }
    defer file.Close()

    fmt.Println("Uploaded file:", handler.Filename)
}
```

---

## 6. Headers (commonly used for auth tokens)

```go
func handleRequest(w http.ResponseWriter, r *http.Request) {
    token := r.Header.Get("Authorization")
    contentType := r.Header.Get("Content-Type")

    fmt.Println(token, contentType)
}
```

---

## Quick Summary

| Type         | Method                           | Common Use            |
| ------------ | -------------------------------- | --------------------- |
| JSON Body    | `json.NewDecoder(r.Body).Decode` | POST/PUT requests     |
| Query Params | `r.URL.Query().Get()`            | Filtering, pagination |
| Path Params  | `r.PathValue()`                  | Resource IDs          |
| Form Data    | `r.FormValue()`                  | HTML forms            |
| Multipart    | `r.FormFile()`                   | File uploads          |
| Headers      | `r.Header.Get()`                 | Auth, content type    |

---

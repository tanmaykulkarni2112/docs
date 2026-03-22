## Sending json as response

Unlike other language, go uses the `structs` alongside json data that is sent.

We create a struct to emulate the json response we want to send, the struct will help define the strucuture beforehand.

```go
type User struct {
    Name string `json:"name"`
    Age int `json:"age"`
}

func sendJson(w http.ResponseWriter, r *http.Request) {
    user := User{
        Name: "tanmay",
        Age: 12
    }
    // converting struct -> json
    // send the json as it is
    w.Header().Set("Content-Type", "application/json")
    json.NewEncoder(w).Encode(user)
}
```

> There might be cases where we need to manipulate the json or
> one of the function signature requires []bytes.

Ideal below are some of the cases where we might require `json.Marshal()`

1. Logging the response
2. Writing to a file
3. Storing in a variable to pass around
4. Comparing or transforming JSON before sending

```go
type Student struct {
    Firstname string `json:"firstname"`
    Lastname string `json:"lastname"`
}

func jsonResponse(w http.ResponseWriter, r *http.Request) {
    student := Student {
        Firsname : "Roy",
        Lastname : "Lee"
    }
    // converting the struct -> []byte
    data , err := json.Marshal(user)
    if err != nil {
        log.Fatal(err)
    }
    w.Header().Set("Content-Type","application/json")
    // handles []byte -> json
    w.Write(data)  // writes JSON-encoded bytes to the HTTP response body
}
```

# GORM V2 paginator

A paginator doing cursor-based pagination based on [GORM v2](https://github.com/go-gorm/gorm)

> Please, checkout release and docs, for introduces some incompatible-API change and many improvements: <br>[GORM 2.0 Release Note](https://gorm.io/docs/v2_release_note.html)

<br>

## Installation

```sh
go get -u github.com/dmitryburov/gorm-paginator
```
<br>

## Usage

- GORM Guides: https://gorm.io

```go
type Book struct {
	gorm.Model
	Title string
}

var (
    dbEntity = db
    paging   = paginator.Paging{}
    bookList = struct {
        Items      []*Book
        Pagination *paginator.Pagination
    }{}
)

// change paging params from query data
// if len(query.Get("limit")) > 0 && query.Get("limit") != "" {
//     paging.Limit, _ = strconv.Atoi(query.Get("limit"))
// }
 
// change DB filters and ect.
// dbEntity.Where("id > ?", 1)

bookList.Pagination, err := paginator.Pages(&paginator.Param{
    DB:     dbEntity,
    Paging: &paging,
}, &bookList.Items)
if err != nil {
    log.Fatal("Error get list: ", err.Error())
}

fmt.Printf("%+v\n", bookList.Items)      // result data
fmt.Printf("%+v\n", booklist.Pagination) // result bookList

```

<br>

## License

[MIT](LICENSE)
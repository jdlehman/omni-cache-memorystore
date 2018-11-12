# OmniCache MemoryStore

An in-memory persistence layer for [omni-cache](https://github.com/panoplymedia/omni-cache).

### Sample Usage

```go
defaultTimeout := time.Minute
gcInterval := time.Minute
cache, err := NewCache(defaultTimeout, gcInterval)
if err != nil {
  fmt.Println(err)
}

// open a connection to badger database
conn, err := cache.Open("") // pass in empty string since the URI is arbitrary
defer conn.Close()

// write data to cache (uses defaultTimeout)
err = conn.Write([]byte("key"), []byte("data"))

// write data to cache with custom timeout
err = conn.WriteTTL([]byte("key2"), []byte("data"), 5*time.Minute)

// read data
data, err := conn.Read([]byte("key"))

// log stats
fmt.Println(conn.Stats())
```

# golimitrate
go-limitrate

##features
*限速，在请求速度过快时，可以限制请求速度，但是不丢失请求

##sample
package main

import (
    "fmt"
    "sync"
    "time"
    "github.com/maoku-go/golimitrate"
)

func main() {
    var wg sync.WaitGroup
    var lr golimitrate.LimitRate
    lr.SetRate(3)
    
    b:=time.Now()
    for i := 0; i < 10; i++ {
        wg.Add(1)
        go func() {
            if lr.Limit() {
                fmt.Println("Got it!")
            }
            wg.Done()
        }()
    }
    wg.Wait()
    fmt.Println(time.Since(b))
}


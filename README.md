# go-micrograd

> :warning: This is a learning resource created from the original [karpathy/micrograd repository](https://github.com/karpathy/micrograd) in Python, and [its amazing lecture in youtube

This reposiository is a simple learning resource about how a Neural Network works in Go programming language, so it does adjust and learn from results. It's only xxx lines of code. However, it's capable of constructing entire deep neural nets for binary classification, as demonstrated in the demo.

**Potential Use Cases:** Primarily educational.

## Installation

```bash
go get github.com/yourusername/gomicrograd
```

## Example Usage

Here's an example showcasing the API and its various supported operations:

```go
package main

import (
    "fmt"
    "github.com/yourusername/gomicrograd/engine"
)

func main() {
    a := engine.NewValue(-4.0)
    b := engine.NewValue(2.0)

    c := a.Add(b)
    d := a.Mul(b).Add(b.Pow(3))

    c = c.Add(c).Add(engine.NewValue(1.0))
    c = c.Add(engine.NewValue(1.0)).Add(c).Sub(a)

    d = d.Add(d.Mul(engine.NewValue(2.0)).Add(b.Add(a).ReLU()))
    d = d.Add(d.Mul(engine.NewValue(3.0)).Add(b.Sub(a).ReLU()))

    e := c.Sub(d)
    f := e.Pow(2.0)
    g := f.Div(engine.NewValue(2.0)).Add(engine.NewValue(10.0).Div(f))

    fmt.Printf("%f\n", g.Data) // prints the result of the forward pass

    g.Backward()

    fmt.Printf("%f\n", a.Grad) // prints dg/da
    fmt.Printf("%f\n", b.Grad) // prints dg/db
}
```

## Training a Neural Net

Refer to the demo file `demo.go` for a complete demonstration on training a 2-layer neural network binary classifier. By initializing a neural net from the `gomicrograd/nn` package, you can implement a straightforward svm "max-margin" binary classification loss and employ SGD for optimization.

## Tracing / Visualization

To assist in understanding the constructed graph, refer to the `trace_graph.go` script which can be used to generate visual representations, demonstrating both the data and the gradient.

## Running Tests

Ensure you have the necessary dependencies and simply run:

```bash
go test ./...
```

## License

MIT

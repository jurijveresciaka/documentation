GO
==

Installation
------------

Download GO from `<https://golang.org/dl/>`_ to **/usr/local/go/bin**.

Configure path:

.. code-block:: shell

    # .bashrc
    export PATH=$PATH:/usr/local/go/bin

Configure workspace
-------------------

GO path
^^^^^^^

.. code-block:: shell

    # .bashrc
    export GOPATH=$HOME/go_path
    export PATH=$PATH:$GOPATH/bin

Workspace
^^^^^^^^^

.. code-block:: shell

    $ mkdir src/github.com/jurijveresciaka

First program
-------------

Create project directory
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: shell

    $ cd src/github.com/jurijveresciaka
    $ mkdir halloworld

Create source code
^^^^^^^^^^^^^^^^^^

.. code-block:: go

    package main

    import "fmt"

    func main() {
	    fmt.Println("Hallo World")
    }

Compile
^^^^^^^

.. code-block:: shell

    $ go install

Run
^^^

.. code-block:: shell

    $ halloworld

First library
-------------

Create lib directory
^^^^^^^^^^^^^^^^^^^^

.. code-block:: shell

    $ cd src/github.com/jurijveresciaka
    $ mkdir -p go/lib/math

Create source code
^^^^^^^^^^^^^^^^^^

.. code-block:: go

    package math

    func IsPrime(n uint64) bool {
      // 0 and 1 not prime.
      if n < 2 {
        return false
      }

      // all even numbers except 2 are no prime.
      if n != 2 && n % 2 == 0 {
        return false
      }

      var i uint64

      for i = 2; i * i <= n ; i++ {
        if n % i == 0 {
          return false
        }
      }

      return true
    }

Compile
^^^^^^^

.. code-block:: shell

    $ go build

Library usage
-------------

.. code-block:: go

    package main

    import (
      "fmt"
      "github.com/jurijveresciaka/go/lib/math"
    )

    func main() {
      fmt.Println(math.IsPrime(12))
    }

Compile
^^^^^^^

.. code-block:: shell

    $ go install

Run
^^^

.. code-block:: shell

    $ halloworld

First test
----------

.. code-block:: go

    package math

    import (
      "testing"
    )

    func TestIsPrime(t *testing.T) {
      type testDataStruct struct {
        number uint64
        isPrime bool
      }

      var testDataList = []testDataStruct{
        {0, false}, {1, false}, {2, true}, {3, true},
        {4, false}, {5, true}, {6, false}, {7, true},
        {8, false}, {9, false},
        {1000000, false},
      }

      for _, testData := range testDataList {
        isPrime := IsPrime(testData.number)

        if isPrime != testData.isPrime {
          t.Errorf("IsPrime(%d) == %q, want %d", testData.number, isPrime, testData.isPrime)
        }
      }
    }

Compile
^^^^^^^

.. code-block:: shell

    $ go build

Run
^^^

.. code-block:: shell

    $ go test

Variables
---------

.. code-block:: go

    package main

    import (
        "fmt"
    )

    func main() {
        var (
            boolean bool = false

            unsignedNumber8 uint8 = 8
            unsignedNumber16 uint16 = 16
            unsignedNumber32 uint32 = 32
            unsignedNumber64 uint64 = 64

            signedNumber8 int8 = -8
            signedNumber16 int16 = -16
            signedNumber32 int32 = -32
            signedNumber64 int64 = -64

            floatNumber32 float32 =  0.32
            floatNumber64 float64 =  -0.64
        )

        fmt.Println(
            boolean,

            unsignedNumber8,
            unsignedNumber16,
            unsignedNumber32,
            unsignedNumber64,

            signedNumber8,
            signedNumber16,
            signedNumber32,
            signedNumber64,

            floatNumber32,
            floatNumber64,
        )
    }

Constants
---------

.. code-block:: go

    package main

    import (
        "fmt"
    )

    func main() {
        const (
            boolean bool = false
        )

        fmt.Println(boolean)
    }

Strings
-------

Basics
^^^^^^

.. code-block:: go

    package main

    import (
        "fmt"
    )

    func main() {
        var (
            name string = "Jurij Veresciaka"
        )

        fmt.Println(name, len(name), name[7], string(name[7]))
    }

Declaration
^^^^^^^^^^^

.. code-block:: go

    package main

    import (
        "fmt"
    )


    func main() {
        var (
            smallText string = "small text"

            largeText string =
            "large text " +
            "large text " +
            "large text"

            rawText string =
    `raw text
    raw text
    raw text`
        )

        fmt.Println(smallText)
        fmt.Println(largeText)
        fmt.Println(rawText)
    }

Convert
^^^^^^^

.. code-block:: go

    package main

    import (
        "fmt"
        "strconv"
    )

    func checkError(err error) {
        if err != nil {
            fmt.Println(err)
        }
    }

    func main() {
        var (
            err error
            boolean bool
            unsignedNumber64 uint64
            signedNumber64 int64
            floatNumber64 float64
        )

        boolean, err = strconv.ParseBool("true")
        checkError(err)
        fmt.Println(boolean);

        unsignedNumber64, err = strconv.ParseUint("64", 10, 64)
        checkError(err)
        fmt.Println(unsignedNumber64);

        signedNumber64, err = strconv.ParseInt("-64", 10, 64)
        checkError(err)
        fmt.Println(signedNumber64);

        floatNumber64, err = strconv.ParseFloat("0.99", 64)
        checkError(err)
        fmt.Println(floatNumber64);

        fmt.Println(strconv.FormatBool(true))
        fmt.Println(strconv.FormatUint(64, 10))
        fmt.Println(strconv.FormatInt(-64, 10))
        fmt.Println(strconv.FormatFloat(-64.123456789123456789, 'E', -1, 64))
    }

Arrays, slices
--------------

General
^^^^^^^

.. code-block:: go

    package main

    import (
        "fmt"
        "reflect"
    )

    func main() {
        var (
            formatString string = "\type => %s; length => %d\n"

            uint64Array1 = [5]uint64{1, 2, 3, 4, 5}
            uint64Array2 = [...]uint64{1, 2, 3, 4, 5}
            uint64Array3 [10]uint64

            uint64Slice1 = []uint64{1, 2, 3, 4, 5}
            uint64Slice2 = []uint64{}
            uint64Slice3 []uint64

            stringArray = [...]string{"one", "two", "three", "four"}
        )

        fmt.Println("ARRAYS:")
        fmt.Printf(formatString, reflect.TypeOf(uint64Array1).Kind(), len(uint64Array1))
        fmt.Printf(formatString, reflect.TypeOf(uint64Array2).Kind(), len(uint64Array2))
        fmt.Printf(formatString, reflect.TypeOf(uint64Array3).Kind(), len(uint64Array3))
        fmt.Println()

        fmt.Println("SLICES:")
        fmt.Printf(formatString, reflect.TypeOf(uint64Slice1).Kind(), len(uint64Slice1))
        fmt.Printf(formatString, reflect.TypeOf(uint64Slice2).Kind(), len(uint64Slice2))
        fmt.Printf(formatString, reflect.TypeOf(uint64Slice3).Kind(), len(uint64Slice3))
        fmt.Println()

        fmt.Println("LOOP (index, value):")
        for index, value := range stringArray {
            fmt.Printf("\t%d => %s\n", index, value)
        }

        fmt.Println("LOOP (value):")
        for _, value := range stringArray {
            fmt.Printf("\t%s\n", value)
        }
    }

Slice from array
^^^^^^^^^^^^^^^^

.. code-block:: go

    package main

    import (
        "fmt"
    )

    func main() {
        var (
            array = [...]uint64{1, 2, 3, 4, 5, 6, 7, 8, 9}
        )
                                 //  0 1 2 3 4 5 6 7 8 9 (index)
        fmt.Println(array[0:5])  // [1 2 3 4 5]
        fmt.Println(array[1:5])  //   [2 3 4 5]
        fmt.Println(array[7:9])  //                 [8 9]
        fmt.Println(array[5:])   //             [6 7 8 9]
        fmt.Println(array[:5])   // [1 2 3 4 5]
        fmt.Println(array[:])    // [0 1 2 3 4 5 6 7 8 9]
    }

Slice append
^^^^^^^^^^^^

.. code-block:: go

    package main

    import (
        "fmt"
    )

    func main() {
        var (
            sliceOne = []uint64{1, 2, 3, 4, 5}
            sliceTwo = []uint64{}

            sliceThree = []uint64{0, 0, 0, 0, 0}
            sliceFour = []uint64{1, 1, 1, 1, 1}
            sliceFive = []uint64{}
        )

        fmt.Println(sliceOne) // [1 2 3 4 5]

        sliceTwo = append(sliceOne, 6, 7, 8, 9, 10)
        fmt.Println(sliceTwo) // [1 2 3 4 5 6 7 8 9 10]

        sliceFive = append(sliceThree, sliceFour...)
        fmt.Println(sliceFive) // [0 0 0 0 0 1 1 1 1 1]
    }

Slice make
^^^^^^^^^^

.. code-block:: go

    package main

    import (
        "fmt"
    )

    func main() {
        var (
            stringFormat string = "length => %d; capacity => %d\n"
            sliceOne = make([]uint64, 0, 5)
            i uint64 = 0
        )

        for i = 0; i < 15; i++ {
            sliceOne = append(sliceOne, i)
            fmt.Printf(stringFormat, len(sliceOne), cap(sliceOne))
        }
    }

Links
-----

`<https://www.gitbook.com/book/astaxie/build-web-application-with-golang/details>`_

`<http://www.dotnetperls.com/go>`_

`<http://golang-book.ru>`_

`<http://alanhollis.com/go-compared-with-php-arrays-and-slices/>`_
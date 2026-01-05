Notes on std::optional

the default constructor & many other for std::optional is constexpr
what are the usecases for these to attributes?

1. constexpr constructor variant allow compile time computation of any logic so long as the arguments can be resolved at compile time
2. since c++20 exceptions can be thrown with constexpr function and constructors
   if at compile time the throw is executed there is compilation error
   if not there is actual correct compilation,
   This helps in creating code paths where at we can check at compile time if there is going to be expections in the path.

```
struct PacketSize {
    int bytes;
    constexpr PacketSize(int b) : bytes(b) {
        if (b % 64 == 0) throw "Invalid";  // C++20: allowed via constexpr if
    }
};

constexpr PacketSize p(128);  // invalid at compile time
constexpr PacketSize p(130);  // valid at compiletime
```

```
struct Point {
  int a;b;
  constexpr Point(int a, int b) : a(a), b(b){}
  constexpr sum(){ return a + b; }
};

constexpr Point p(2, 3);
constexpr s = p.sum();
```


constexpr destructors
allowing constexper destructors in C++20 opened doors to write compile time programs which look like regular c++
because it enable RAII,
Even though at compile time there is no allocation or deallocation we can still use mapping of offest and bound time 
to objects thus achieveing RAII.

https://yongweiwu.wordpress.com/2024/10/11/cxx-compile-time-programming/?utm_source=chatgpt.com

Contexpr has now with C++20 has become powerful enough to bypass template meta programming magic, 
now I don't have to write those crypting template meta programming techiniques
I can just use for, if, while and a lot of stl algorithms to get evaluated at compile time.


what are the usecases for constructors being noexcept

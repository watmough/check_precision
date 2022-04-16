# check_precision

Simple templated function to identify whether two floating point numbers are sufficiently similar.

```C++
#include <algorithm>
#include <cmath>
#include <limits>

#if DEBUG
    #include <iostream>
    #define DB(x) x
#else
    #define DB(x)
#endif

template<typename Tfloating, unsigned char significant_digit_loss> 
struct check_precision {
    bool operator()(Tfloating left, Tfloating right) const {
        // verify that floating point values left and right differ only by
        // ::epsilon x 10 ^ significant digits allowed to be lost
        // https://stackoverflow.com/a/17382806/33758
        constexpr 
        Tfloating scale       = std::pow(10.0, significant_digit_loss) * 
                                std::numeric_limits<Tfloating>::epsilon();
        Tfloating difference  = std::abs(left - right);
        Tfloating allowable   = scale *
                                std::max(std::abs(left), std::abs(right));
        DB(std::cout << "left: " << left << " right: " << right << std::endl;)
        DB(std::cout << "difference: " << difference 
                     << " allowable: " << allowable << std::endl;)
        return difference < allowable;
    }
};

inline constexpr check_precision<float,  1> 
        check_same;

int main() {
    auto retval = check_same( 123456001000.0,
                              123456131000.0);
    return retval;
}
```


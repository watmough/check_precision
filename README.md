# check_precision

Simple templated function to identify whether two floating point numbers are sufficiently similar.

(Code on Godbolt)[https://godbolt.org/#z:OYLghAFBqd5QCxAYwPYBMCmBRdBLAF1QCcAaPECAMzwBtMA7AQwFtMQByARg9KtQYEAysib0QXACx8BBAKoBnTAAUAHpwAMvAFYTStJg1DIApACYAQuYukl9ZATwDKjdAGFUtAK4sGe1wAyeAyYAHI%2BAEaYxCAAzFykAA6oCoRODB7evnrJqY4CQSHhLFEx8baY9vkMQgRMxASZPn4JdpgO6bX1BIVhkdFxrXUNTdlD3b3FpYMAlLaoXsTI7BwmGgCC5rHByN5YANQmsW5iwCSECCxH2GubZtsMu14HR27ILEwECNe3Wzt7mEOx1oeBYhAUPw2v3ueCo%2BwAItgLHIAOK3fYYw4wx4AoFuJwKAjETCsSHrTFY2JYGghBEWCCqGb7VTQ2KVJTozFbanBQHw%2BmM1muWG/DYETAsRIGcWvAgAT0SjFYgIAKlRaKhPsFgKR9l4GKlgCF0PtkAh6vtDQxYXhRIIAPr4YCEe0ahQQ2LYQ4bQnELwOU0IdoAa3tiWJyDwqQEhwA7FYNhSIqhPPtUIriJ8SBAZhA1RqtUZ9vQqARdfnNY4i8Q8MAEAQmWgDQQ4wnyRTMQB6Tv7ABu0Vhcv2X0%2B%2B3Vle1%2B2SwRbvbEXkwCmLmFL%2B0MJprdZb%2BCoVGiaYYtCHETlnI7%2B27%2BxAIEwiVSGoYzP2XA0hwArF6rTa7dva%2BC17QGoAO6YCaRD7FExYpAQZ4dpe9YEHeIDdoSTDIMGqD9sQ45AQAdGgLCdkwnZcLGsQABxmORGgAGydrEsSxm%2B5GwRSTaEpgqjht67bnhWhbAJaoj0OeQLwpaBDoNeyRARAL64RoupfjQP6On%2BBCuikChMgAVDxokGYZBmElJIAMD4A7IK6oLgq8/FVsA1zXre94CDmRxtgZ9mTjue7Eo8gJiRJplMBECgQCWLYALT7Ju9YzB5rGYt5RZiMBoUiRiRziQowmAjpSVGUVHYmdeHyqBApUgKF4WRXMwXXjVEBxQ2CWxJ5on8pVknXmgXgtq8rxYmYkUgMNeJDZFE3HONLVjeYZjTW4sW1vWS0NTeDDoLQHkJYmnX0lVfUDccQ0Lb50SMMs81mItg0zRd/nLPpxUGfdy0LQB6UROI43vV9qBARlgL/VVrg7e1e28R2xIEIsj6PVdIMzWlgPA4l%2B1ZbG8K/NjGObBswQgrS7HilxxCBiGYYRlG6SvOOny6s%2B1wveeZpUwoyr47cM77B8wQ5q2sFMP1qCxZgBBzrQQXs%2Bh9qc2wEDPvckhvjRGgaC%2BGsKaQhWvUZXAq2rXDxBrGgKW1HUYrD8Pi5LYjc3jGwcHMtCcG%2BvB%2BBwWikKgnBuNY1iWgsSwg/cPCkAQmgu3MQZMFgMQ5qQwYgG%2Biluxwki8CwEga6QXs%2B37HC8AoICKVH3su6QcCwDAiAoKgkp0NE5CUARiTNzEwDkbEfB0OKxClxAETR6QETBPUcqcBHBFsIIADyh5T5XpBYB8RjiCv%2BARo4/alyvnHtP1KwRzOlSjyCESZsQcoeFgo9EqC09V%2BqTDAAoABqeCYEB8%2BKl7Ed%2BCCBEGIdgUgZCCEUCodQK9dAJAMEYFAgdLD6DwGFeAcx0zVH3lFEy2VTCWGsKRfYUV56xBIfCREyIUQl0qO0aoLgtqjBaKQQIvIpgDASLkNIAhmE5BSDwhgkx%2BgxFaHQjoAgugjE8M0PQbQJE1GGD0dhIi5FKL4eMBowiSicLmAoEO10EhEkwCfKuGcPb51HkXVQ5EaJRRopIfYwBkDIH2ORXC5CIAB0ISg/YuBCAkEpAkfYHgm70AplsLgMxeAVy0DMWOJIE6UDmCnNO%2BhOBZ1IDnNJBdeBFxLmXSO0c5g13rofZAosyAUAgPUd%2ByhDCVCEAgQGADeDtzoFqAQ9SQi0CaS00e7TwkgG7r3QZ0R579T6UBXJrDVDtHWMQd%2BnBeDlNqPgL2vAgHCDyhIaQWyoFqFHnA/QhhjDIJsJfUukBMGJGwZwXBkl8HnOIaQ8hUVKFIlRCXAxYDbCSWCN0xpzTpnP0jsSUxpAgKZkSM/V27tPZWM4NgOZFSiAUxsXYhxTiXFuI8fsLx5zdT%2BLRUE6JRTK7xNIHHJJScM6ZOyYpGZ%2BTbCFNiTHZOqd06cFiAilezK2WUozmYXlhdlnkriXMLC0Y/CSCAA%3D%3D%3D]


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


# sbg-provider
This is a dead simple library that serves the purpose of providing values, no matter if it comes from a value, a functor, a lamda of a function pointer. The advantage of using this library is it breaks no API (in most cases).

### How?

It behaves like a functor, but it doesn't break your API! You can keep sending values as parameters, but you will be able to send function and functors too!
Take this example without Provider:
    
    using namespace std;
    
    void displayMe(double d) {
        cout << d << endl;
    }
    
    int main() {
        
        // shows 6.7 in the terminal
        displayMe(6.7);
        
        // displayMe([]{ return 8.1; }) error
        
        return 0;
    }
    
Now, with Provider:

    using namespace std;
    using namespace sbg;
    
    void displayMe(Provider<double> d) {
        cout << d() << endl;
    }
    
    int main() {
        
        // shows 6.7 in the terminal
        displayMe(6.7);
        
        // it works! shows 8.1
        displayMe([]{ return 8.1; }) 
        
        return 0;
    }
    
Here's some good new! It work great with returns too:

    
    using namespace std;
    
    function<int()> makeSomething(bool sw) {
        if (sw) {
            // getTicks is a function that returns a value by the time
            // This value changes, it's okay to return a function
            return []{ return getTicks() * 2 };
        } else {
            // Not so great syntax to return a number
            return []{ return 8.1 };
        }
    }

Now with Provider:
    
    using namespace std;
    using namespace sbg;
    
    Provider<int> makeSomething(bool sw) {
        if (sw) {
            // getTicks is a function that returns a value by the time
            // This value changes, it's okay to return a function
            return []{ return getTicks() * 2 };
        } else {
            // Wow, that's better!
            return 8.1;
        }
    }
    
The better thing here is that in all those example, no external refactor was needed. You can just change your function parameters and return values and you can use functor or values as parameter and return type right away!

The only case you can break your APIs is when you change ( for T as a type ) a function with a T return type to a Provider<T>.

## Getting Started
### biicode users
If you want to use Provider, just include it!
    
    #include "gracicot/sbg-provider/provider.h"
    
### Other users

You just have to download the header, configure your project/IDE and use it!

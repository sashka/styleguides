C++ code style guides
======================

Code formatting
-------------------
1. Always save in UTF-8.

2. Spaces should be used for indentation. Indent with tabs are only when absolutely required (i.e. Makefile).

3. Indentation width should be 2 or 4 whitespaces. Use uniform indentation within a single file. If author uses 4 whitespaces then you should stick with that.

4. Code inside `namespace` should not be indented. Always add a comment with namespace name after a closing bracket.

   _Correct:_

	   namespace mediaplanner {

	   class Config {
	       Config();
	       ...
	   };

	   } // namespace mediaplanner


   _Incorrect:_

	   namespace mediaplanner {

	       class Config {
	           Config();
	           ...
	       };

	   } // namespace mediaplanner

5. Code inside `class`, `enum`, `struct` etc. should be indented.

   _Correct:_

		class SimpleConfig {
			SimpleConfig();
			...
		};


   _Incorrect:_

        class Config {
        Config();
        ...
        };

6. Keywords such as `public`, `protected`, `private` inside a class should be indented at the same level as a class definition and should appear in the following order: `public`, `protected` and `private`.

    _Correct:_

        class Accessor {
        public:
          ...

        protected:
          ...

        private:
          ...
        };


    _Incorrect:_

        class Accessor {
          protected:
            ...

          public:
            ...

          private:
            ...
        };


Whitespaces
-------
1. Do not use whitespaces with unary operators.

    _Correct:_

        ++i;
        i++;


    _Incorrect:_

        i ++;
        ++ i;


2. Binary and ternary operators should be embraced by whitespaces. Whitespace should also follow after a comma.

    _Correct:_

        y = m * x + b;
        c =  a | b;
        f(x, y);
        return condition ? 1 : 0;


    _Incorrect:_

        y = m*x+b;
        c =  a|b;
        f(x,y);
        return condition ? 1:0;


3. There should be a whitespace between opening keyword and a parenthesis.

    _Correct:_

        if (condition) {
            Action();
        }


    _Incorrect:_

        if(condition) {
            Action();
        }


4. Do not use whitespace between function name and parenthesis.

    _Correct:_

        f(a, b);

    _Incorrect:_

        f (a, b);
        f( a, b );


5. There should be no whitespace between a base type and "*" or "&" in case of a pointer or reference type.

    _Correct:_

        Document* LoadDocument(const FilePath& path);


    _Incorrect:_

        Document *LoadDocument(const FilePath &path);
        Document * LoadDocument(const FilePath & path);


Newlines
-------------
1. Every expression needs it's own line.

    _Correct:_

        ++x;
        y++;
        if (condition) {
            Action();
        }


    _Incorrect:_

        ++x; y++;
        if (condition) { Action(); }


Curly brackets
---------------
1. Opening curly bracket should always be at the end of a line preceeding corresponding code block. Closing bracket needs it's own line.

    _Correct:_

        class Storage {
            Storage(string& filename);
            ...
        };

        namespace threads {
            ...
        };

        for (int i = 0; i < 10; ++i) {
            Action();
        }


    _Incorrect:_

        class Storage
        {
            Storage(string& filename);
            ...
        };

        for (int i = 0; i < 10; ++i)
        {
            Action();
        }


2. Always use brackets, even if a code block is empty.

    _Correct:_

        for (int i = container->begin(); i != container->end(); ++i) {
        }


    _Incorrect:_

        for (int i = container->begin(); i != container->end(); ++i);


Using NULL, false and 0
-----------------------------
1. Always use `NULL` for null pointers in C and C++, `0` for integer, `0.0` for floating point, and`'\0'` for char.

2. bool values should always be `true` and `false`. Support for bool type in C in included in `base/basictypes.h`.

3. Null pointer tests should always be explicit.

    _Correct:_

        Vector* ptr = new Vector();
        if (ptr == NULL) {
            Abort("Everything goes bad");
            ...
        };


    _Incorrect:_

        if (!ptr) {
            ...
        };

4. Boolean tests are implicit.

    _Correct:_

        bool condition = true;
        if (condition) {
            ...
        };

    _Incorrect:_

        if (condition == true) {
            ...
        };

5. Test for zero must be explicit.

    _Correct:_

        int n;
        if (n == 0) {
            ...
        };

		float f;
        if (f != 0.0) {
            ...
        };


    _Incorrect:_

        if (n) {
            ...
        };

        if (!f) {
            ...
        };


Macros
-------
1. Don't use macros where you can avoid them.

2. Use `const` instead of `#define` for constants.

3. Use inline functions instead of macros.

4. Macros should be typed in all _caps_ to visually distinguish them from methods and variables. In case of multiple words split then with underscore "_".

    _Correct:_

        #define DEFINE_PROPERTY(key, val) wxConvCurrent->cWX2MB(key, val)

    _Incorrect:_

        #define define_property(key, val) wxConvCurrent->cWX2MB(key, val)
        #define DefineProperty(key, val) wxConvCurrent->cWX2MB(key, val);


Constants and enumerations
------------------------
1. Constant names should look like this: `kDaysInWeek`. Articles and other insignificant language constructs should be excluded.

2. Enumeration values should either follow constant naming rules (`kError404NotFound`) or macros naming rules (`ERROR_404_NOT_FOUND`).


Default method parameters
------------------------------
1. Default parameters should only be defined in header files.

    _Correct:_

        class A {
        public:
          void Hello(const std::string& message="Hi!");
        };

    _Incorrect:_

        void A::Hello(const std::string& message = "Hi!") {
          ...
        }

2. Do not set default parameters for virtual methods. There's always a risc of them being inherited from a parent class.

    _Example:_

        class A {
        public:
            virtual void bla(int x = 1);
        };

        class B : public A {
        public:
            void bla(int x = 2);
        };

        A a = B();
        a.bla(); // принимает x = 1



Further reading
===============
[Google C++ Style Guide](http://google-styleguide.googlecode.com/svn/trunk/cppguide.xml)

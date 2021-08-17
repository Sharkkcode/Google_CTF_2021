# HEXAGON

- Throw the file into r2, we can see the functions.

    ![]()

- goto entry0

    ![]()

- goto loc.read_flag

    ![]()

- goto loc.flag

    ![]()

- goto loc.check_flag

    ![]()

- goto loc.hex1 to loc.hex6

    ![]()

- There is only some simple calculation, so I use z3 to solve this. But I failed... By reading [This_writeup](), I found that some commands must be executed in parallel.
- By checking debug info, these commands must be executed in parallel. So I modified my code and get the flag.

    ![]()

- Code:
    ```python
    ```



# HEXAGON

- Throw the file into r2, we can see the functions.

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/functions.png)

- goto entry0

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/entry0.png)

- goto loc.read_flag

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/read_flag.png)

- goto loc.flag

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/flagdata.png)

- goto loc.check_flag

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/check_flag.png)

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/check_flag_2.png)

- goto loc.hex1 to loc.hex6

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/hex1.png)

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/hex2.png)

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/hex3.png)

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/hex4.png)

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/hex5.png)

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/hex6.png)

- There is only some simple calculation, so I use z3 to solve this. But I failed... By reading [This_writeup](https://github.com/cscosu/ctf-writeups/tree/master/2021/google_ctf/hexagon), I found that some commands must be executed in parallel.
- By checking debug info, these commands must be executed in parallel. So I modified my code and get the flag.

    ![](https://github.com/Sharkkcode/Google_CTF_2021/blob/main/HEXAGON/imgs/parallel.png)

- Code:

```python
from z3 import *

s = z3.Solver()

N = 8

x = [z3.BitVec(f'x{i}', 8) for i in range(N)]
print("x:", x)

R2 = z3.Concat(*x[0:4][::-1])
R3 = z3.Concat(*x[4:8][::-1])
# print("R2:", R2)
# print("R3:", R3)

R0 = z3.BitVecVal(1869029418, 32)
# print("R0:", R0)

# swap
R0, R2 = R2, R0
# print("R0:", R0)
# print("R2:", R2)

R1 = z3.BitVecVal(1, 32)
# print("R1:", R1)

# hex1
R5 = z3.BitVecVal(173879092, 32)
R0 = R0 + R5
# print("R0:", R0)
R0 = z3.BitVecVal(-1, 32) - R0
# print("R0:", R0)

R2 = R2 ^ R0
# print("R2:", R2)
R0 = z3.BitVecVal(1701603183, 32)

# swap
R0, R3 = R3, R0

R1 = z3.BitVecVal(6, 32)

# hex2
R0 = z3.BitVecVal(-1, 32) - R0
R5 = z3.BitVecVal(1210484339, 32)
R0 = R0 ^ R5

R3 = R3 ^ R0
R0 = z3.BitVecVal(1852400160, 32)
R1 = z3.BitVecVal(15, 32)

# hex3
R5 = z3.BitVecVal(1519522183, 32)
R0 = R0 ^ R5
R5 = z3.BitVecVal(-373614660, 32)
R0 = R0 + R5
R0 = R0 ^ R3
R2, R3 = R3, (R2 ^ R0)

R0 = z3.BitVecVal(1747804522, 32)
R1 = z3.BitVecVal(28, 32)

# hex4
R0 = z3.BitVecVal(-1, 32) - R0
R5 = z3.BitVecVal(-686802991, 32)
R0 = R0 ^ R5

R0 = R0 ^ R3
R2, R3 = R3, (R2 ^ R0)

R0 = z3.BitVecVal(1734441061, 32)
R1 = z3.BitVecVal(45, 32)

# hex5
R0 = z3.BitVecVal(-1, 32) - R0
R5 = z3.BitVecVal(270515404, 32)
R0 = R0 + R5

R0 = R0 ^ R3
R2, R3 = R3, (R2 ^ R0)

R0 = z3.BitVecVal(706768495, 32)
R1 = z3.BitVecVal(66, 32)

# hex6
R5 = z3.BitVecVal(-1962843199, 32)
R0 = R0 ^ R5
R5 = z3.BitVecVal(-288476533, 32)
R0 = R0 ^ R5

R0 = R0 ^ R3
R2, R3 = R3, (R2 ^ R0)

R4 = z3.BitVecVal(0x6d80bf97, 32)
R5 = z3.BitVecVal(0x9d450e3d, 32)


s.add(R5 == R3)
s.add(R4 == R2)

s_check = s.check()
if s_check == sat:
	print(s_check)
	m = s.model()
	for i in range(N):
		print(chr(m[x[i]].as_long()), end='')
else:
	print(s_check)

print()
```



# CPP

- A file with a lot of macros: [cpp.c]()
- Turn the code to some language the we can debug with computer. Here is my full code: [python_c.py]()
- By analyzing the code I found that there is a lot of 0~7s, so I assume that they are some byte-like data. ex: SOMETHING_0~SOMTHING_7 is a byte.
- If we can execute the program into "if S==58", then S will become -1. That means (S != -1) isn't true and we will go to the main function. (The input will be our flag)

- Code segment at bellow tells us that byte Q must be 0 everytime.

```
if S == 56:
	if S != 0:
		S = 0
	S = 57
	if Q0 == 0:
		if Q1 == 0:
			if Q2 == 0:
				if Q3 == 0:
					if Q4 == 0:
						if Q5 == 0:
							if Q6 == 0:
								if Q7 == 0:
									if S != 0:
										S = 0
									S = 58
if S == 57:
	if S != 0:
		S = 0
	S = 58
	print("INVALID_FLAG")
	break
if S == 58:
	if S != 0:
		S = 0
	S = 59
	if S != 0:
		S = 0
	S = -1
	get_flag = True
	break
```

- Then after that the program will turn A to 1 and add it to I.

```
if S == 53:
	if S != 0:
		S = 0
	S = 54
	A0 = 1
	if A1 != 0:
		A1 = 0
	if A2 != 0:
		A2 = 0
	if A3 != 0:
		A3 = 0
	if A4 != 0:
		A4 = 0
	if A5 != 0:
		A5 = 0
	if A6 != 0:
		A6 = 0
	if A7 != 0:
		A7 = 0
if S == 54:
	if S != 0:
		S = 0
	S = 55
	if c != 0:
		c = 0
	if I0 == 0:
		if A0 == 0:
			if c  != 0:
				I0 = 1
				if c != 0:
					c = 0
		else:
			if c == 0:
				I0 = 1
				if c != 0:
					c = 0
	else:
		if A0 == 0:
			if c  != 0:
				if I0 != 0:
					I0 = 0
				c = 1
		else:
			if c == 0:
				if I0 != 0:
					I0 = 0
				c = 1
	if I1 == 0:
		if A1 == 0:
			if c  != 0:
				I1 = 1
				if c != 0:
					c = 0
		else:
			if c == 0:
				I1 = 1
				if c != 0:
					c = 0
	else:
		if A1 == 0:
			if c  != 0:
				if I1 != 0:
					I1 = 0
				c = 1
		else:
			if c == 0:
				if I1 != 0:
					I1 = 0
				c = 1
	if I2 == 0:
		if A2 == 0:
			if c  != 0:
				I2 = 1
				if c != 0:
					c = 0
		else:
			if c == 0:
				I2 = 1
				if c != 0:
					c = 0
	else:
		if A2 == 0:
			if c  != 0:
				if I2 != 0:
					I2 = 0
				c = 1
		else:
			if c == 0:
				if I2 != 0:
					I2 = 0
				c = 1
	if I3 == 0:
		if A3 == 0:
			if c  != 0:
				I3 = 1
				if c != 0:
					c = 0
		else:
			if c == 0:
				I3 = 1
				if c != 0:
					c = 0
	else:
		if A3 == 0:
			if c  != 0:
				if I3 != 0:
					I3 = 0
				c = 1
		else:
			if c == 0:
				if I3 != 0:
					I3 = 0
				c = 1
	if I4 == 0:
		if A4 == 0:
			if c  != 0:
				I4 = 1
				if c != 0:
					c = 0
		else:
			if c == 0:
				I4 = 1
				if c != 0:
					c = 0
	else:
		if A4 == 0:
			if c  != 0:
				if I4 != 0:
					I4 = 0
				c = 1
		else:
			if c == 0:
				if I4 != 0:
					I4 = 0
				c = 1
	if I5 == 0:
		if A5 == 0:
			if c  != 0:
				I5 = 1
				if c != 0:
					c = 0
		else:
			if c == 0:
				I5 = 1
				if c != 0:
					c = 0
	else:
		if A5 == 0:
			if c  != 0:
				if I5 != 0:
					I5 = 0
				c = 1
		else:
			if c == 0:
				if I5 != 0:
					I5 = 0
				c = 1
	if I6 == 0:
		if A6 == 0:
			if c  != 0:
				I6 = 1
				if c != 0:
					c = 0
		else:
			if c == 0:
				I6 = 1
				if c != 0:
					c = 0
	else:
		if A6 == 0:
			if c  != 0:
				if I6 != 0:
					I6 = 0
				c = 1
		else:
			if c == 0:
				if I6 != 0:
					I6 = 0
				c = 1
	if I7 == 0:
		if A7 == 0:
			if c  != 0:
				I7 = 1
				if c != 0:
					c = 0
		else:
			if c == 0:
				I7 = 1
				if c != 0:
					c = 0
	else:
		if A7 == 0:
			if c  != 0:
				if I7 != 0:
					I7 = 0
				c = 1
		else:
			if c == 0:
				if I7 != 0:
					I7 = 0
				c = 1
```

- May be there is a loop through every char input and check if Q is 0 every iteration?

```
// Maybe???
for(int i = 0; i < flag_length; i++) {
    // Some code
    if(Q == 0) {
        // Some code
    }
}
// goto 58
```

- I add some check point to the python code base on this assumption, and it WORKS! I got the flag!

```
# if byte Q isn't 0 then go back
if not (Q0 == 0 and Q1 == 0 and Q2 == 0 and Q3 == 0 and Q4 == 0 and Q5 == 0 and Q6 == 0 and Q7 == 0):
	# print("not correct")
	ss = ss[:i] + chr(ord(ss[i])+1) + ss[i+1:]
	i -= 1
	break
else:
	if count_depth == i:
		# print("correct")
		flag += ss[i]
		break
	count_depth += 1
```

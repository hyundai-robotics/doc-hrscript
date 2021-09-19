# 6.1.2 Examples

Refer to the following examples of usage.

```python
do2=1		# Turns on the bit output value of number 0 of fb0
fb2.dob3=0b00001111  	# Designates the 3rd byte output value of fb2 as a binary bit string
fb[4].dob1=0x0F  	# Turns on the lower 4 bits of the 1st byte output value of fb4, and turns off the upper 4 bits
var work_no=fb9.dib3    # Assigns the 3rd byte input value of fb9 to the work_no variable
if fb5.di43 then *err  	# Branches to the *err label when fb5.di42 is turned on
for idx=21 to 29
  fb3.do[idx]=1  	# Turns on all output signals do21 ~ do29 of fb3 
next
fb2.do3=fb2.do7=fb2.do11=1   # Turns on 3rd, 7th, and 11th output signals of fb2 at once
```


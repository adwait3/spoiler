# spoiler

first we see the img file in hex ed and see it is a reversed elf 


![image](https://github.com/adwait3/spoiler/assets/148553626/58899b5b-7caf-4e26-8377-360731b1393e)

so we use this script to get the elf 

```
def reverse_file_bytes(input_file_path, output_file_path):
    try:
        # Open the input file in binary read mode
        with open(input_file_path, 'rb') as input_file:
            # Read the entire file into a byte array
            data = input_file.read()

        # Reverse the byte array
        reversed_data = data[::-1]

        # Open the output file in binary write mode
        with open(output_file_path, 'wb') as output_file:
            # Write the reversed byte array to the output file
            output_file.write(reversed_data)
        
        print(f"Reversed file bytes have been written to {output_file_path}")
    
    except FileNotFoundError:
        print(f"The file {input_file_path} does not exist.")
    except IOError as e:
        print(f"An IOError occurred: {e}")

# Example usage
input_file_path = '/home/kali/Desktop/SPOILER_img.jpg'
output_file_path = '/home/kali/Desktop/out'
reverse_file_bytes(input_file_path, output_file_path)
```

i use ida to dissasemble the code and then use gpt to help with z3 to help with the z3 script 

```
from z3 import *

# Define the integer variables
a1 = Int('a1')
a2 = Int('a2')
a3 = Int('a3')
a4 = Int('a4')

# Create a solver instance
solver = Solver()

# Add the constraints from the function
solver.add(3 * a4 + a3 + 4 * a2 - 10 * a1 == 28)
solver.add(9 * a2 - 8 * a1 + 6 * a3 - 2 * a4 == 72)
solver.add(a4 - 3 * a2 - 2 * a1 - 8 * a3 == 29)
solver.add(a3 + 5 * a1 + 7 * a2 - 6 * a4 == 88)

# Check if there is a solution
if solver.check() == sat:
    model = solver.model()
    a1_val = model[a1].as_long()
    a2_val = model[a2].as_long()
    a3_val = model[a3].as_long()
    a4_val = model[a4].as_long()
    print(f'Solution found:')
    print(f'a1 = {a1_val}')
    print(f'a2 = {a2_val}')
    print(f'a3 = {a3_val}')
    print(f'a4 = {a4_val}')
else:
    print('No solution found')

```

this gives me the solution 

![image](https://github.com/adwait3/spoiler/assets/148553626/83716915-a4e0-44bb-8a0f-9c2fea12e4df)

![image](https://github.com/adwait3/spoiler/assets/148553626/7ecb37c3-e39a-4cd6-b5fc-902450f2466d)


# flag 
`N0PS{r1CKUNr0111N6}`


```python

from itertools import permutations

def convert_to_number(s, letter_to_digit):
    num = 0
    for ch in s:
        num = num * 10 + letter_to_digit[ch]
    return num

def is_valid_assignment(operands, result, letter_to_digit):
    sum_ = sum(convert_to_number(operand, letter_to_digit) for operand in operands)
    result_number = convert_to_number(result, letter_to_digit)
    return sum_ == result_number

def solve_cryptarithmetic(operands, result):
    letters = set(''.join(operands) + result)
    
    if len(letters) > 10:
        return False  
    
    letter_list = list(letters)
    
    for perm in permutations(range(10), len(letter_list)):
        letter_to_digit = {letter_list[i]: perm[i] for i in range(len(letter_list))}
        
       
        if any(letter_to_digit[operand[0]] == 0 for operand in operands) or letter_to_digit[result[0]] == 0:
            continue
        
        if is_valid_assignment(operands, result, letter_to_digit):
            print_solution(operands, result, letter_to_digit)
            return True
    
    return False

def print_solution(operands, result, letter_to_digit):
    print("Letter-to-Digit Mapping:")
    for letter, digit in letter_to_digit.items():
        print(f"{letter} = {digit}")
    
    print("\nNumber Representations:")
    print("Operands:")
    for operand in operands:
        print(f"{operand} -> {convert_to_number(operand, letter_to_digit)}")
    print(f"Result:")
    print(f"{result} -> {convert_to_number(result, letter_to_digit)}")

if __name__ == "__main__":
    operands = ["SEND", "MORE"]
    result = "MONEY"
    
    solvable = solve_cryptarithmetic(operands, result)

```
    if not solvable:
        print("No solution exists.")

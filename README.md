
# signed-binary-arithmetic-
def to_8bit(n):
    return format(n & 0xFF, '08b')


def from_8bit(binary):
    value = int(binary, 2)

    if value & 0x80:
        value -= 256

    return value


def signed_add(a, b):
    binary_a = to_8bit(a)
    binary_b = to_8bit(b)

    result_binary = format(
        (int(binary_a, 2) + int(binary_b, 2)) & 0xFF,
        '08b'
    )

    result = from_8bit(result_binary)

    # Overflow occurs when operands have same sign
    # but result has different sign
    overflow = ((a >= 0 and b >= 0 and result < 0) or
                (a < 0 and b < 0 and result >= 0))

    return binary_a, binary_b, result_binary, result, overflow


# Expression 1
a, b = 25, 18
x, y, r, value, overflow = signed_add(a, b)

print("Expression 1: 25 + 18")
print("25  =", x)
print("18  =", y)
print("Result =", r)
print("Decimal Result =", value)
print("Overflow =", overflow)

print()

# Expression 2
a, b = -25, -18
x, y, r, value, overflow = signed_add(a, b)

print("Expression 2: -25 + (-18)")
print("-25 =", x)
print("-18 =", y)
print("Result =", r)
print("Decimal Result =", value)
print("Overflow =", overflow)
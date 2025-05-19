How to Run
Use the Go Live extension to run the project.
(Install the "Live Server" extension in VS Code and click the Go Live button in the bottom bar.)

Example of Working Code

addi $t3, $zero, 8        # $t3 = 8 (target loop counter)
addi $t4, $zero, 0        # $t4 = 0 (will be used as an address offset)
addi $t5, $zero, 0        # $t5 = 0 (loop counter)
addi $t0, $zero, 2        # $t0 = 2 (initial value to be multiplied)
sw $t0, 0($zero)          # Memory[0] = $t0 (2)

# 0x00000010: This is the loop start address
addi $t4, $t4, 4          # $t4 = $t4 + 4 (address offset incremented)
addi $t5, $t5, 1          # $t5 = $t5 + 1 (increment loop counter)
mult $t5, $t0             # Multiply $t5 by $t0
mflo $t1                  # Move the result of multiplication to $t1
sw $t1, 0($t4)            # Store $t1 at Memory[$t4]
bne $t3, $t5, 0x00000010  # If $t3 != $t5, branch to 0x00000010 (start of the loop)
j 0x00000020              # Jump to the end (exit the loop)

### Exercício 01

Traduza o seguinte programa para a linguagem Assembly do MIPS.

Em python:
```python
a = 0

while(True):
    if a > 0:
        break
    else:
        a += 1
```

Em Assembly MIPS:
```assembly
ADDI $s0, $zero, 0
Loop:
    SLTI $t0, $s0, 10
    BEQ $t0, $zero, Exit 
    ADDI $s0, $s0, 1
    J Loop
Exit:
```

### Exercício 02
Escreva a seguinte função na linguagem Assembly do MIPS. Considere que as variáveis n1, n2, n3 e n4 terão seus valores armazenados em registradores do tipo $s0, $s1, $s2 e $s3. Portanto, os valores originais desses registradores devem ser carregados na pilha de execução (Stack) quando a função for executada e, após a execução da função, os valores originais devem ser restaurados a esses registradores.

Em python:
```python
def foo(a, b):
    n1 = 10
    n2 = 20
    n3 = 30
    n4 = 40
    r1 = a * (n1 + n2)
    r2 = b * (n3 - n4)
    return r1, r2
```

Em Assembly MIPS:
```assembly
 foo:
    ADDI $sp, $sp, -24
    
    SW $a0, 20($sp)
    SW $a1, 16($sp)
    
    SW $s0, 12($sp)
    SW $s1, 8($sp)
    SW $s2, 4($sp)
    SW $s3, 0($sp)
    
    ADDI $s0, $zero, 10
    ADDI $s1, $zero, 20
    ADDI $s2, $zero, 30
    ADDI $s3, $zero, 40
    
    ADD $t0, $s0, $s1
    SUB $t1, $s2, $s3
    
    MUL $v0, $a0, $t0
    MUL $v1, $a1, $t1
    
    LW $a0, 20($sp)
    LW $a1, 16($sp)
    
    LW $s0, 12($sp)
    LW $s1, 8($sp)
    LW $s2, 4($sp)
    LW $s3, 0($sp)
    
    ADDI $sp, $sp, 24
    JR $ra
```
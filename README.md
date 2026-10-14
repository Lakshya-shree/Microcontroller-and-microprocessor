; 16-bit Division using Repeated Subtraction
; Dividend = 1357H
; Divisor  = 0025H

LXI H,1357H       ; HL = Dividend
LXI D,0025H       ; DE = Divisor
LXI B,0000H       ; BC = Quotient

DIV:  MOV A,L
      SUB E
      MOV L,A

      MOV A,H
      SBB D
      JC DONE

      MOV H,A

      INX B         ; Quotient = Quotient + 1
      JMP DIV

DONE: SHLD 5100H    ; Remainder → 5100H (LSB), 5101H (MSB)

      MOV A,C
      STA 5102H     ; Quotient LSB
      MOV A,B
      STA 5103H     ; Quotient MSB

      HLT

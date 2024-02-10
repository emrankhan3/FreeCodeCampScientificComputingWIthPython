# FreeCodeCampScientificComputingWIthPython

# project 1
```py
  def arithmetic_arranger(problems,flag=False):

  if len(problems) > 5:
    return 'Error: Too many problems.'
  operators = [problem.split()[1] for problem in problems]
  if not all(operator in ['+','-'] for operator in operators):
    return "Error: Operator must be '+' or '-'."
  operands1 = [problem.split()[0] for problem in problems]    
  operands2 = [problem.split()[2] for problem in problems]
  if not all(operand.isdigit() for operand in operands1+operands2):
    return 'Error: Numbers must only contain digits.'
  if not all(len(operand) < 5 for operand in operands1+operands2):
    return 'Error: Numbers cannot be more than four digits.'
  max_lengths = [max(len(operands1[i]),len(operands2[i]) ) for i in range(len(operands2))]
  arranged_problems = ''

  #operands1 arrangement
  for i in range(len(problems)):
    s = f'%{max_lengths[i]+2}s'%operands1[i]
    arranged_problems+=s
    if i!=len(problems)-1:
      arranged_problems+="    "
  arranged_problems+='\n'
  kk = ' '.join(arranged_problems)

  #operands2 and operator arrangment 
  for i in range(len(problems)):
    s = f'%{max_lengths[i]+1}s'%operands2[i]
    s = operators[i]+s
    arranged_problems+=s
    if i!=len(problems)-1:
      arranged_problems+="    "
  arranged_problems+='\n'
  tl=0

  for i in range(len(problems)):
    l = max_lengths[i]+2
    s = l*'-'
    arranged_problems+=s
    if i!=len(problems)-1:
      arranged_problems+="    "

  
 
 # print(s)
  ans=[int(operands1[i]) + int(operands2[i]) if operators[i] == '+'
       else int(operands1[i]) - int(operands2[i]) for i in range(len(problems))]
  if flag:
    arranged_problems+='\n'
    for i in range(len(problems)):
      s = f'%{max_lengths[i]+2}s'%str(ans[i])
      arranged_problems+=s
      if i!=len(problems)-1:
        arranged_problems+="    "
  
  return arranged_problems
``

# FreeCodeCampScientificComputingWIthPython

# Arithmetic_Arranger
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
```
# Time Calculator

```py
  def add_time(start, duration,today=''):
  weeks = ['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday','Sunday']
  start_time = start.split()[0]
  ampm = start.split()[1]
  start_hour = int(start_time[:start_time.find(':')])
  start_minute = int(start_time[start_time.find(':')+1:])
  if(ampm=='PM'):
    start_hour+=12
  d_hour = int(duration[:duration.find(':')])
  d_minute = int(duration[duration.find(':')+1:])
  
  actual_duration = d_hour*60+d_minute

  current_time = (start_hour*60+start_minute + actual_duration)%(60*24)
  current_h = int(current_time/60)
  
  current_h12 = current_h%12
  if current_h12==0:
    current_h12=12
  current_m = int(current_time%60)

  # fix am or pm
  if current_h<12:
    ampm='AM'
  else:
    ampm='PM'
  days = int((start_hour*60+start_minute + actual_duration)/(60*24))
  # print(days)
  dayStr=''
  if days >0:
    if days==1:
      dayStr = ' (next day)'
    else:
      dayStr = f' ({days} days later)'
  week=''
  if today!='':
    today = today.lower().capitalize()
    idx = weeks.index(today)
    idx = (idx+days)%7
    week = f', {weeks[idx]}'
  new_time = f'{current_h12}:{current_m:02} {ampm}{week}{dayStr}'
  print(new_time)
  


  return new_time
```
# BudgetApp
```py
  class Category:
  
  def __init__(self,name):
    self.name = name
    self.ledger =[]
    self.balance = 0.0
    self.spent = 0.0
  def deposit(self,amount,description=''):
    self.ledger.append({"amount":amount,"description":description})
    self.balance += amount
  def withdraw(self,amount,description=''):
    if self.check_funds(amount):
      self.ledger.append({"amount":-amount,"description":description})
      self.balance -= amount
      self.spent += amount
      return True
    else:
      return False
  def transfer(self,amount,rec):
    if self.check_funds(amount):
      self.withdraw(amount,"Transfer to "+rec.name)
      rec.deposit(amount,"Transfer from "+self.name)
      return True
    else:
      return False
  def get_balance(self):
    return self.balance
    
  def check_funds(self,amount):
    return self.balance >= amount
  def __str__(self):
    s = self.name.center(30,"*")+"\n"
    for i in self.ledger:
      s+=i["description"][:23].ljust(23)+str("{:.2f}".format(i["amount"])).rjust(7)+"\n"
    s+="Total: "+str(self.balance)
    return s


def create_spend_chart(categories):
  total = 0
  #return str(len(categories))
  spent = []
  for category in categories:
    total += category.spent
  for category in categories:
    val = (category.spent*100)//total 
   
    spent.append(val)
    
  chart = "Percentage spent by category\n"
  for i in range(100,-1,-10):
    chart += str(i).rjust(3) + '| '
    for percent in spent:
      if percent >= i:
        chart += 'o  '
      else:
        chart += '   '
    chart += '\n'
  chart += '    ' + '-' * (len(categories) * 3 + 1) + '\n'
  max_len = 0
  #-----------------------------------------------------
  for category in categories:
    if len(category.name) > max_len:
      max_len = len(category.name)
  for i in range(max_len):
    chart += '     '
    for category in categories:
      if len(category.name) > i:
        chart += category.name[i] + '  '
      else:
        chart += '   '
    if i < max_len - 1:
      chart += '\n'
  return chart

```

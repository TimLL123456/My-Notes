# The Python Debugger

**PDB** is Python's built-in interactive debugger. It's incredibly powerful for tracking down bugs without adding countless print statements.
* Similar function in VSCode Debugger

## Flash Card
```text
Basic Commands:
  n, next      - Execute next line
  s, step      - Step into function
  c, continue  - Continue execution
  l, list      - Show code context
  p, print     - Print variable
  pp           - Pretty print
  whatis       - Check data type
  q, quit      - Quit debugger

Variable Inspection:
  a, args      - Function arguments
  w, where     - Stack trace
  u, up        - Move up stack
  d, down      - Move down stack

Breakpoints:
  b lineno     - Set breakpoint
  b function   - Break at function
  cl           - Clear breakpoints
```

## Sample Code
```python
import pdb

def process_user_data(user_data, config):
    pdb.set_trace()  # Start debugging here
    # breakpoint     # It works in other python version
    
    # Let's say we're not sure what keys exist
    user_id = user_data['id']
    username = user_data['username']
    email = user_data.get('email', 'default@example.com')
    
    # Process with config
    theme = config['ui']['theme']
    
    return f"Processing {username} with {theme} theme"

# Sample data that might cause issues
user_data = {'id': 123, 'name': 'John'}  # Missing 'username'
config = {'ui': {'color': 'blue'}}  # Missing 'theme'

result = process_user_data(user_data, config)
```

## Code Execution
use for not setting breakpoint
```bash
>>> python -m pdb main.py
```

## Debugging
```python
PS C:\Users\tllam\Downloads> python -m pdb .\test.py # Start debugging
> c:\users\tllam\downloads\test.py(1)<module>()
-> def process_user_data(user_data, config):
(Pdb) n # Execute next line
> c:\users\tllam\downloads\test.py(14)<module>()
-> user_data = {'id': 123, 'name': 'John'}  # Missing 'username'
(Pdb) c # Continue execution
Traceback (most recent call last):
  File "C:\EUC_Program\Python\Python37\lib\pdb.py", line 1697, in main
    pdb._runscript(mainpyfile)
  File "C:\EUC_Program\Python\Python37\lib\pdb.py", line 1566, in _runscript
    self.run(statement)
  File "C:\EUC_Program\Python\Python37\lib\bdb.py", line 585, in run
    exec(cmd, globals, locals)
  File "<string>", line 1, in <module>
  File "c:\users\tllam\downloads\test.py", line 14, in <module>
    user_data = {'id': 123, 'name': 'John'}  # Missing 'username'
  File "c:\users\tllam\downloads\test.py", line 5, in process_user_data
    username = user_data['username']
KeyError: 'username'
Uncaught exception. Entering post mortem debugging
Running 'cont' or 'step' will restart the program
> c:\users\tllam\downloads\test.py(5)process_user_data()
-> username = user_data['username']
(Pdb) p user_data.keys() # Print variable
dict_keys(['id', 'name'])
(Pdb) whatis user_data # Check data type
<class 'dict'>
(Pdb)
```

# BlitzActions

is a framework to translate text prompts to function executions

## Installation

```bash
pip install blitzactions
```

## Usage

```python
from os import environ
from dotenv import load_dotenv, find_dotenv
load_dotenv(find_dotenv())

from blitzactions.manager import ActionsManager

data = [
    {
        "name": "Joshua",
        "sales": 100000,
        "profit": 10000,
        "payment": 1000,
    },
    {
        "name": "Rudra",
        "sales": 300000,
        "profit": 30000,
        "payment": 3000,
    },
    {
        "name": "Vishal",
        "sales": 200000,
        "profit": 20000,
        "payment": 2000,
    }
]

manager = ActionsManager(environ.get('OPENAI_API_KEY'))

@manager.register
def generate_employee_report(employee_name: str) -> str:
    """Generates report of employee with name passed in employee_names"""
    return f'Employee name: {employee_name}\nSales: {data[0]["sales"]}\nProfit: {data[0]["profit"]}\nPayment: {data[0]["payment"]}'

@manager.register
def show_employee_data() -> str:
    """Generates a report of all employees with all details in the table"""
    return '\n'.join([f'{d["name"]} | {d["sales"]} | {d["payment"]}' for d in data])

@manager.register
def execute_payments_to_employees() -> int:
    """Processes payroll payments to all employees for this month"""
    for employee in data:
        print(f'Processing {employee["payment"]}USD payment for {employee["name"]}')


result = manager.execute(input("Enter your prooompt: "))
print(result)
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change. /s


---
aliases: []
---
```py

```

Библиотека для сериализации и десериализации данных.
Сериализация - от сложного к простому, десериализация - от простого к сложному.

Созданим простой класс и его экземпляр:
```py
class Person:  
    def __init__(self, name, age):  
        self.name = name  
        self.age = age  
  
    def __repr__(self):  
        return f'{self.name} is {self.age} years old.'  
input_data = {}  
  
input_data['name'] = 'Julia'  
input_data['age'] = 32  
  
person = Person(name=input_data['name'], age=input_data['age'])  
print(person)

>>> Julia is 32 years old.
```

Для работы с Marshmallow необходимо создать схему:
```py
class PersonSchema(Schema):
    name = fields.String()
    age = fields.Integer()

    @post_load # для десериализации
    def create_person(self, data, **kwargs):
        return Person(**data)

>>> 
```

Попробуем применить схему к данным:
```py
from marshmallow import Schema, fields, post_load

class Person:
    def __init__(self, name, age):
        self.name = name 
        self.age = age 

    def __repr__(self):
        return f'{ self.name } is { self.age } years old.'

class PersonSchema(Schema):
    name = fields.String()
    age = fields.Integer()

    @post_load
    def create_person(self, data, **kwargs):
        return Person(**data)

input_data = {}

input_data['name'] = input('What is your name? ')
input_data['age'] = input('What is your age? ')

schema = PersonSchema()
result = schema.load(input_data)


print(result)

```


помимо сериализации и десериализации библиотекой можно пользоваться как **валидатором**.

Немного перепишем класс:
```py
from marshmallow import Schema, fields, post_load, ValidationError

class Person:
    def __init__(self, name, age, email):
        self.name = name 
        self.age = age
        self.email = email

    def __repr__(self):
        return f'{ self.name } is { self.age } years old.'
		
class PersonSchema(Schema):
    name = fields.String()
    age = fields.Integer()
    email = fields.Email()
	
	@post_load
    def create_person(self, data, **kwargs):
        return Person(**data)
	
input_data = {}

input_data['name'] = input('What is your name? ')
input_data['age'] = input('What is your age? ')
input_data['email'] = input('What is your email? ')

try:
    schema = PersonSchema()
    person = schema.load(input_data)
	result = schema.dump(person)
    print(result)
except ValidationError as err:
    print(err)
```

https://www.youtube.com/watch?v=YgguC8p5B24
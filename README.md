<div align="center">
<img alt="Alx logo" src="https://assets.imaginablefutures.com/media/images/ALX_Logo.max-200x150.png">
</div>

# 0x00. AirBnB clone - The console

---

![AirBnB Logo](https://www.pngitem.com/pimgs/m/132-1322125_transparent-background-airbnb-logo-hd-png-download.png)
<h1 align="center">AirBnB</h1>

<p align="center">
  <img src="https://github.com/bdbaraban/AirBnB_clone/blob/master/assets/hbnb_logo.png" alt="HolbertonBnB logo">
</p>
<h1 align="center">HolbertonBnB</h1>

<p align="center">An AirBnB Clone Project.</p>

---

## Description :house:

A Team project to build a clone of [AirBnB](https://www.airbnb.com/).
This is the first part of the AirBnB clone project where we worked on the backend of the project whiles interfacing it with a console application with the help of the cmd module in python.
Data (python objects) generated are stored in a json file and can be accessed with the help of the json module in python.
The console is a command interpreter to manage objects abstraction between objects and how they are stored.
To see the fundamental background of the project visit the [Wiki](https://github.com/ralexrivero/AirBnB_clone/wiki).

HolbertonBnB is a complete web application, integrating database storage, a back-end API, and front-end interfacing in a clone of AirBnB.
The project currently only implements the back-end console.
The console will perform the following tasks:

* create a new object
* retrive an object from a file
* do operations on objects
* destroy an object

## Classes :cl:

HolbertonBnB utilizes the following classes:

|     | BaseModel | FileStorage | User | State | City | Amenity | Place | Review |
| --- | --------- | ----------- | -----| ----- | -----| ------- | ----- | ------ |
| **PUBLIC INSTANCE ATTRIBUTES** | `id`<br>`created_at`<br>`updated_at` | | Inherits from `BaseModel` | Inherits from `BaseModel` | Inherits from `BaseModel` | Inherits from `BaseModel` | Inherits from `BaseModel` | Inherits from `BaseModel` |
| **PUBLIC INSTANCE METHODS** | `save`<br>`to_dict` | `all`<br>`new`<br>`save`<br>`reload` | "" | "" | "" | "" | "" | "" |
| **PUBLIC CLASS ATTRIBUTES** | | | `email`<br>`password`<br>`first_name`<br>`last_name`| `name` | `state_id`<br>`name` | `name` | `city_id`<br>`user_id`<br>`name`<br>`description`<br>`number_rooms`<br>`number_bathrooms`<br>`max_guest`<br>`price_by_night`<br>`latitude`<br>`longitude`<br>`amenity_ids` | `place_id`<br>`user_id`<br>`text` | 
| **PRIVATE CLASS ATTRIBUTES** | | `file_path`<br>`objects` | | | | | | |

## Storage :baggage_claim:

The above classes are handled by the abstracted `Storage` engine defined in the 
[FileStorage](./models/engine/file_storage.py) class.

Every time the backend is initialized, HolbertonBnB instantiates an instance of 
`FileStorage` called `storage`. The `storage` object is loaded/re-loaded from 
any class instances stored in the JSON file `file.json`. As class instances are 
created, updated, or deleted, the `storage` object is used to register 
corresponding changes in the `file.json`.

## Console :computer:

The console is a command line interpreter that permits management of the backend 
of HolbertonBnB. It can be used to handle and manipulate all classes utilized by 
the application (achieved by calls on the `storage` object defined above).

### Using the Console

The HolbertonBnB console can be run both interactively and non-interactively. 
To run the console in non-interactive mode, pipe any command(s) into an execution 
of the file `console.py` at the command line.

```
$ echo "help" | ./console.py
(hbnb) 
Documented commands (type help <topic>):
========================================
EOF  all  count  create  destroy  help  quit  show  update

(hbnb) 
$
```

Alternatively, to use the HolbertonBnB console in interactive mode, run the 
file `console.py` by itself:

```
$ ./console.py
```

While running in interactive mode, the console displays a prompt for input:

```
$ ./console.py
(hbnb) 
```

To quit the console, enter the command `quit`, or input an EOF signal 
(`ctrl-D`).

```
$ ./console.py
(hbnb) quit
$
```

```
$ ./console.py
(hbnb) EOF
$
```

### Console Commands

The AirBnB or HolbertonBnB console supports the following commands:

> And are displayed in the following format: *Command / usage / example with output*

* **create**
  * Usage: `create <class>`

> *Creates a new instance of a given class. The class' ID is printed and the instance is saved to the file `file.json`.*

```
$ ./console.py
(hbnb) create BaseModel
119be863-6fe5-437e-a180-b9892e8746b8
(hbnb) quit
$ cat file.json ; echo ""
{"BaseModel.119be863-6fe5-437e-a180-b9892e8746b8": {"updated_at": "2019-02-17T2
1:30:42.215277", "created_at": "2019-02-17T21:30:42.215277", "__class__": "Base
Model", "id": "119be863-6fe5-437e-a180-b9892e8746b8"}}
```

* **show**
  * Usage: `show <class> <id>` or `<class>.show(<id>)`

> *Prints the string representation of a class instance based on a given id.*

```
$ ./console.py
(hbnb) create User
1e32232d-5a63-4d92-8092-ac3240b29f46
(hbnb)
(hbnb) show User 1e32232d-5a63-4d92-8092-ac3240b29f46
[User] (1e32232d-5a63-4d92-8092-ac3240b29f46) {'id': '1e32232d-5a63-4d92-8092-a
c3240b29f46', 'created_at': datetime.datetime(2019, 2, 17, 21, 34, 3, 635828), 
'updated_at': datetime.datetime(2019, 2, 17, 21, 34, 3, 635828)}
(hbnb) 
(hbnb) User.show(1e32232d-5a63-4d92-8092-ac3240b29f46)
[User] (1e32232d-5a63-4d92-8092-ac3240b29f46) {'id': '1e32232d-5a63-4d92-8092-a
c3240b29f46', 'created_at': datetime.datetime(2019, 2, 17, 21, 34, 3, 635828), 
'updated_at': datetime.datetime(2019, 2, 17, 21, 34, 3, 635828)}
(hbnb) 
```
* **destroy**
  * Usage: `destroy <class> <id>` or `<class>.destroy(<id>)`

> *Deletes a class instance based on a given id. The storage file `file.json` is updated accordingly.*

```
$ ./console.py
(hbnb) create State
d2d789cd-7427-4920-aaae-88cbcf8bffe2
(hbnb) create Place
3e-8329-4f47-9947-dca80c03d3ed
(hbnb)
(hbnb) destroy State d2d789cd-7427-4920-aaae-88cbcf8bffe2
(hbnb) Place.destroy(03486a3e-8329-4f47-9947-dca80c03d3ed)
(hbnb) quit
$ cat file.json ; echo ""
{}
```

* **all**
  * Usage: `all` or `all <class>` or `<class>.all()`

> *Prints the string representations of all instances of a given class. If no class name is provided, the command prints all instances of every class.*

```
$ ./console.py
(hbnb) create BaseModel
fce2124c-8537-489b-956e-22da455cbee8
(hbnb) create BaseModel
450490fd-344e-47cf-8342-126244c2ba99
(hbnb) create User
b742dbc3-f4bf-425e-b1d4-165f52c6ff81
(hbnb) create User
8f2d75c8-fb82-48e1-8ae5-2544c909a9fe
(hbnb)
(hbnb) all BaseModel
["[BaseModel] (450490fd-344e-47cf-8342-126244c2ba99) {'updated_at': datetime.da
tetime(2019, 2, 17, 21, 45, 5, 963516), 'created_at': datetime.datetime(2019, 2
, 17, 21, 45, 5, 963516), 'id': '450490fd-344e-47cf-8342-126244c2ba99'}", "[Bas
eModel] (fce2124c-8537-489b-956e-22da455cbee8) {'updated_at': datetime.datetime
(2019, 2, 17, 21, 43, 56, 899348), 'created_at': datetime.datetime(2019, 2, 17,
21, 43, 56, 899348), 'id': 'fce2124c-8537-489b-956e-22da455cbee8'}"]
(hbnb)
(hbnb) User.all()
["[User] (8f2d75c8-fb82-48e1-8ae5-2544c909a9fe) {'updated_at': datetime.datetim
e(2019, 2, 17, 21, 44, 44, 428413), 'created_at': datetime.datetime(2019, 2, 17
, 21, 44, 44, 428413), 'id': '8f2d75c8-fb82-48e1-8ae5-2544c909a9fe'}", "[User] 
(b742dbc3-f4bf-425e-b1d4-165f52c6ff81) {'updated_at': datetime.datetime(2019, 2
, 17, 21, 44, 15, 974608), 'created_at': datetime.datetime(2019, 2, 17, 21, 44,
15, 974608), 'id': 'b742dbc3-f4bf-425e-b1d4-165f52c6ff81'}"]
(hbnb) 
(hbnb) all
["[User] (8f2d75c8-fb82-48e1-8ae5-2544c909a9fe) {'updated_at': datetime.datetim
e(2019, 2, 17, 21, 44, 44, 428413), 'created_at': datetime.datetime(2019, 2, 17
, 21, 44, 44, 428413), 'id': '8f2d75c8-fb82-48e1-8ae5-2544c909a9fe'}", "[BaseMo
del] (450490fd-344e-47cf-8342-126244c2ba99) {'updated_at': datetime.datetime(20
19, 2, 17, 21, 45, 5, 963516), 'created_at': datetime.datetime(2019, 2, 17, 21,
45, 5, 963516), 'id': '450490fd-344e-47cf-8342-126244c2ba99'}", "[User] (b742db
c3-f4bf-425e-b1d4-165f52c6ff81) {'updated_at': datetime.datetime(2019, 2, 17, 2
1, 44, 15, 974608), 'created_at': datetime.datetime(2019, 2, 17, 21, 44, 15, 97
4608), 'id': 'b742dbc3-f4bf-425e-b1d4-165f52c6ff81'}", "[BaseModel] (fce2124c-8
537-489b-956e-22da455cbee8) {'updated_at': datetime.datetime(2019, 2, 17, 21, 4
3, 56, 899348), 'created_at': datetime.datetime(2019, 2, 17, 21, 43, 56, 899348
), 'id': 'fce2124c-8537-489b-956e-22da455cbee8'}"]
(hbnb) 
```

* **count**
  * Usage: `count <class>` or `<class>.count()`

> *Retrieves the number of instances of a given class.*

```
$ ./console.py
(hbnb) create Place
12c73223-f3d3-4dec-9629-bd19c8fadd8a
(hbnb) create Place
aa229cbb-5b19-4c32-8562-f90a3437d301
(hbnb) create City
22a51611-17bd-4d8f-ba1b-3bf07d327208
(hbnb) 
(hbnb) count Place
2
(hbnb) city.count()
1
(hbnb) 
```

* **update**
  * Usage: `update <class> <id> <attribute name> "<attribute value>"` or
`<class>.update(<id>, <attribute name>, <attribute value>)` or `<class>.update(
<id>, <attribute dictionary>)`.

> *Updates a class instance based on a given id with a given key/value attribute 
pair or dictionary of attribute pairs. If `update` is called with a single 
key/value attribute pair, only "simple" attributes can be updated (ie. not 
`id`, `created_at`, and `updated_at`). However, any attribute can be updated by 
providing a dictionary.*

```
$ ./console.py
(hbnb) create User
6f348019-0499-420f-8eec-ef0fdc863c02
(hbnb)
(hbnb) update User 6f348019-0499-420f-8eec-ef0fdc863c02 first_name "Holberton"
(hbnb) show User 6f348019-0499-420f-8eec-ef0fdc863c02
[User] (6f348019-0499-420f-8eec-ef0fdc863c02) {'created_at': datetime.datetime(
2019, 2, 17, 21, 54, 39, 234382), 'first_name': 'Holberton', 'updated_at': date
time.datetime(2019, 2, 17, 21, 54, 39, 234382), 'id': '6f348019-0499-420f-8eec-
ef0fdc863c02'}
(hbnb)
(hbnb) User.update(6f348019-0499-420f-8eec-ef0fdc863c02, address, "98 Mission S
t")
(hbnb) User.show(6f348019-0499-420f-8eec-ef0fdc863c02)
[User] (6f348019-0499-420f-8eec-ef0fdc863c02) {'created_at': datetime.datetime(
2019, 2, 17, 21, 54, 39, 234382), 'address': '98 Mission St', 'first_name': 'Ho
lberton', 'updated_at': datetime.datetime(2019, 2, 17, 21, 54, 39, 234382), 'id
': '6f348019-0499-420f-8eec-ef0fdc863c02'}
(hbnb)
(hbnb) User.update(6f348019-0499-420f-8eec-ef0fdc863c02, {'email': 'holberton@h
olberton.com', 'last_name': 'School'})
[User] (6f348019-0499-420f-8eec-ef0fdc863c02) {'email': 'holberton@holberton.co
m', 'first_name': 'Holberton', 'updated_at': datetime.datetime(2019, 2, 17, 21,
54, 39, 234382), 'address': '98 Mission St', 'last_name': 'School', 'id': '6f34
8019-0499-420f-8eec-ef0fdc863c02', 'created_at': datetime.datetime(2019, 2, 17,
21, 54, 39, 234382)}
(hbnb) 
```

## Testing :straight_ruler:

Unittests for the HolbertonBnB project are defined in the [tests](./tests) 
folder. To run the entire test suite simultaneously, execute the following command:

```
$ python3 unittest -m discover tests
```

Alternatively, you can specify a single test file to run at a time:

```
$ python3 unittest -m tests/test_console.py
```

## Authors :black_nib:

[Ani Obinna Benzeal](https://www.linkedin.com/in/engraniobc/) | [Twitter](https://twitter.com/AniBenzeal) | [GitHub](https://github.com/mrbenzeal)

*Natnael Feleke* - [Github](https://github.com/NatiBoy33)  

## Credit

<details>
    <summary>Esteban De La Hoz</summary>
    <ul>
    <li><a href="https://www.github.com/Esteban1891">Github</a></li>
    <li><a href="https://www.twitter.com/Esteban18911">Twitter</a></li>
    <li><a href="https://www.linkedin.com/in/esteban-de-la-hoz-romero-b6270017b/">Linkedin</a></li>
    </ul>
</details>
<details>
    <summary>Eduardo Vega</summary>
    <ul>
    <li><a href="https://www.github.com/EduardoVega04">Github</a></li>
    <li><a href="https://www.twitter.com/eduardo_vega04">Twitter</a></li>
    </ul>
</details>
<details>
    <summary>Ayomide Suara</summary>
    <ul>
    <li><a href="https://www.github.com/aysuarex">Github</a></li>
    <li><a href="https://www.twitter.com/Aysuarex">Twitter</a></li>
    <li><a href="mailto:aysuarex@gmail.com">e-mail</a></li>
    </ul>
</details>
<details>
    <summary>Bamidele Adefolaju</summary>
    <ul>
    <li><a href="https://www.github.com/lexxyla">Github</a></li>
    <li><a href="https://www.twitter.com/lexxyla">Twitter</a></li>
    <li><a href="mailto:bamideleadefolaju@gmail.com">e-mail</a></li>
    </ul>
</details>
<details>
    <summary>Tolulope Fakunle</summary>
    <ul>
    <li><a href="https://www.github.com/Tolulope05">Github</a></li>
    <li><a href="https://www.twitter.com/FakunleTolu">Twitter</a></li>
    <li><a href="mailto:fakunletolulope05@gmail.com">Gmail</a></li>
    <li><a href="https://www.linkedin.com/in/tolutech/">Linkedin</a></li>
    <li><a href="https://wa.link/4clrdv">Whatsapp</a></li> 
    </ul>
</details>

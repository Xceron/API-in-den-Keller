# API-in-den-Keller

API wrapper for app-in-den-keller.de

## Requirements

- [Python 3.4+](https://www.python.org)
- ```pip install -r requirements.txt```

## Usage

```python
wohnheim = Api(house)
```

### Available arguments for house

- "Wohnanlage Tarforst - Haus I"
- "Wohnanlage Tarforst - Haus IV"
- "Wohnanlage Tarforst - Haus VIII"
- "Wohnanlage Kleeburger Weg"
- "Wohnanlage Petrisberg"
- "Wohnanlage Martinskloster"
- "Wohnanlage Olewig"

Note that all arguments are case sensitive

### Available methods

| Name                  | Description                                                  | Return type |
| --------------------- | ------------------------------------------------------------ | ----------- |
| all_washers           | returns all washers with their machine number and their time | dict        |
| all_dryers            | returns all dryers with their machine number and their time  | dict        |
| all_machines          | returns all machines with their machine number and their time | dict        |
| all_available_washers | returns all washers which aren't running                     | tuple       |
| all_available_dryers  | returns all dryers which aren't running                      | tuple       |

### Example Usage

```python
wohnheim_olewig = Api("Wohnheim Olewig")
dryers = wohnheim_olewig.all_available_dryers
washers = wohnheim_olewig.all_available_washers
```



## Credits & Licence

Under [MIT LICENCE](https://github.com/Xceron/API-in-den-Keller/blob/master/LICENSE).

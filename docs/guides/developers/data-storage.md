---
title: Data Storage
after: using-decompiler
---

# Data Storage

## Configuration/user data file

As previously mentioned in the section [My first plugin](./my-first-plugin), configuration and user data file use `Newtonsoft.Json` to serialize data structure.
Configuration files are stored in  `./oxide/config folder` and
User data files are stored in  `./oxide/data`. 
But default path can be modified to save in subfolder.  

the basic data structure 
```csharp
private class Configuration
{
	public string ReplyMessage;
}
```
will be serialised to
```json
{
	"ReplyMessage" : "a simple reply message"
}
```
Using the variable name as the key, which is not good for readability and clarity.  
Best practice is to use [NewtonSoft serialization attributes](https://www.newtonsoft.com/json/help/html/SerializeObject.htm) for clarity the information given to the user.Most commonly use attributes :
```csharp
private class PluginData
{
	[JsonProperty(PropertyName = "A simple message when player spawn")]
	public string ReplyMessage;
	
	// Add some info about default value
	// or possible range of the data
	[JsonProperty(PropertyName = "Maximum health value (default=100)")]
	public int MaxHealth = 100;
	
	// because sometime you need data that does not need to be saved
	[JsonIgnore]  
	public Vector3 Position;

	// Here, ObjectCreationHandling is required, 
	// to avoid initialisation data to be added over and over, each time plugin restart.
	[JsonProperty(PropertyName = "Zones to prevent something", ObjectCreationHandling = ObjectCreationHandling.Replace)]
	public List<string> Zones = new List<string> { "KeepOut" };	
}
```

and previous sample code will serialize to:

```json
{
	"A simple message when player spawn" : "a simple reply message",
	"Maximum health value (default=100)" : 100,
	"Zones to prevent something" : [
		"KeepOut"
		]
}
```


## Language data file

The language file is initialized in the LoadDefaultMessages hook. All new message definition will be stored in a file in the `./oxide/lang/(Language code)/(Plugin name).json`.
Only the missing messages are added but does not overwrite the one already existing. This allows server owners to customize messages to their preference.
Server owners can also translate messages to other languages. for example, messages could be translated into Italian and saved in the `./oxide/lang/it/(Plugin name).json` file.  
Note: To revert to the default messages, just delete the file `./oxide/lang/en/(Plugin name).json`.  
``` csharp
private new void LoadDefaultMessages()
{
	lang.RegisterMessages(new Dictionary<string, string>
	{
		["MSG1"]  = "English string 1",
		["MSG2"]  = "English string 2",
		...
	}, this, "en");

	lang.RegisterMessages(new Dictionary<string, string>
	{
		["MSG1"]  = "Localised string for message 1",
		["MSG2"]  = "Localised string for message 2",
	}, this, "fr");
	
	// ... other languages	
}
```

Ex: The previous test code would initialize a file ./oxide/lang/en/test.json that can be customized by server owners.
```json
{
  "MSG1": "English string 1",
  "MSG2": "English string 1",
}
```

Sample code to retrieving translated message from the language file using the lang.GetMessage function.
``` csharp
private string Lang(string key, string id = null, params object[] args) => string.Format(lang.GetMessage(key, this, id), args);
```

### Language code per country/language
| Country | Language code | Country | Language code | Country | Language code |
| :---------------- | :------: | :---------------- | :------: | :---------------- | :------: |
| Afrikaans        | af    | Arabic        | ar   | Catalan          | ca    |
| Czech            | cs    | Denmark       | da   | Deutsch          | de    |
| Greek            | el    | English       | en   | Pirate english   | en-pt |
| Spanish          | es-ES | Finland       | fi   | French           | fr    |
| Hebrew           | he    | Hungarian     | hu   | Italian          | it    |
| Japan            | ja    | Korea         | ko   | Netherland       | nl    |
| Norwegian        | no    | Polish        | pl   | Portuguese Brazil | pt-BR |
| Portuguese Portugal | pt-PT | Romania       | ro   | Russia       | ru    |
| Serbian          | sr    | Swedish       | sv   | Turkish          | tr    |
| Ukrainian        | uk    | Vietnamese    | vi   |                  |       |
| Simplified Chinese | zh-CN | Traditional Chinese |  zh-TW   |        |       |


## Protobuf storage

Protobuf store data in a binary format. Main advantage is a more compact and faster data storage, with the disadvantage to not be human readable like JSON.

`[ProtoContract]`  : to indicates that this class will serialize.  
`[ProtoMember(N)]` : where N represents the number in which order it will serialize  
`[ProtoIgnore]`    : this field will not be serialized.  

### Protobuf class sample

``` csharp
[ProtoContract]
public class sample {
    [ProtoMember(1)]
    public string data1;
    [ProtoMember(2)]
    public List<int> data2;
    [ProtoMember(3)]
    public DateTime data3;
    [ProtoIgnore]
    public int data4;
}
```
### Protobuf Loading
``` csharp
sample mySample
if (ProtoStorage.Exists(filename))
{
	mySample = ProtoStorage.Load<sample>(filename) ?? new sample();
}
else
{
	mySample = new sample();
}
```
### Protobuf Saving
``` csharp
ProtoStorage.Save(mySample, filename);
```


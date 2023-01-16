# Open Notify API clients

A list of OpenNotify API clients written in different languages.

- [.NET](https://github.com/iArmanKarimi/Open-Notify-API-.net)
- [Elixir](https://github.com/iArmanKarimi/Open-Notify-API-elixir)
- [Go](https://github.com/iArmanKarimi/Open-Notify-API-go)
- [JavaScript/TypeScript](https://github.com/iArmanKarimi/Open-Notify-API-js)
- [Python](https://github.com/iArmanKarimi/Open-Notify-API-python)
<!-- - [Rust](https://github.com/iArmanKarimi/Open-Notify-API-rust) -->
  <!-- - [Perl]() -->
  <!-- - [Ruby]() -->
  <!-- - [Haskell]() -->

## Base structure (interface)

Server response:

```ts
interface ISSLocation {
  message: string;
  date_time: DateTime;
  location: {
    latitude: double;
    longitude: double;
  };
}
interface PeopleInSpace {
  number: uint;
  message: string;
  people: Array<{ name: string; craft: string }>;
}
```

Module:

```ts
class OpenNotify {
  public static getISSLocation(): Async<ISSLocation>;
  public static getPeopleInSpace(): Async<PeopleInSpace>;
}
```

Names can be camel case, snake case, etc which are modified in order to match the target language's standards.

## Examples

<details>
<summary>Python</summary>

### ISS Location

```python
iss_location = open_notify.get_ISS_location()
print("ISS location:")
print("latitude:", iss_location.location.latitude)
print("longitude:", iss_location.location.longitude)
```

### People In Space

```python
people_in_space = open_notify.get_people_in_space()
for people in people_in_space.people:
    print(f"craft: {people.craft}, name: {people.name}")
```

</details>
<!-- <details>
<summary>Rust</summary>

### ISS Location

### People In Space

</details> -->
<details>
<summary>Elixir</summary>

### ISS Location

```elixir
  case OpenNotifyApi.get_iss_location() do
    {:ok, iss_location} ->
      IO.puts("Current location of International Space Station:")
      IO.puts("latitude: \#{iss_location.latitude}")
      IO.puts("longitude: \#{iss_location.longitude}")

      iss_location["timestamp"]
      |> DateTime.from_unix()
      |> case do
        {:ok, date_time} -> "Date and time: \#{date_time}" |> IO.puts()
      end

    {:error, error} ->
      IO.inspect(error)
  end
```

### People In Space

```elixir
  case OpenNotifyApi.get_people_in_space() do
    {:ok, people_in_space} ->
      number = people_in_space["number"]
      IO.puts("There are \#{number} people in space right now.")

      people = people_in_space["people"]
      IO.puts("List of people in space:")

      for person <- people do
        name = person["name"]
        craft = person["craft"]
        IO.puts("name: \#{name}, craft: \#{craft}")
      end

    {:error, error} ->
      IO.puts(error)
  end
```

</details>
<details>
<summary>Go</summary>

### ISS Location
```go
iss, err := GetISSLocation()
fmt.Println("current location of ISS:")
fmt.Printf("latitude: %f\n", iss.Location.Latitude)
fmt.Printf("longitude: %f\n", iss.Location.Longitude)
```

### PeopleInSpace
```go
ppl, err := GetPeopleInSpace()
fmt.Println("People in space right now:")
for _, v := range ppl.People {
    fmt.Printf("Craft: %s, Name: %s\n", v.Craft, v.Name)
}
fmt.Printf("Number of people in space: %d\n", ppl.Number)
```

</details>
<details>
<summary>.NET</summary>

### **C#**

### ISS Location

```cs
var iss_loc = await OpenNotify.GetISSLocation();
var output =
  $"International Space Station's Location:\n"
  + $"DateTime: {iss_loc?.DateTime.ToLocalTime()}\n"
  + $"Latitude: {iss_loc?.Location?.Latitude}\n"
  + $"Longitude: {iss_loc?.Location?.Longitude}\n"
 ;
Console.Write(output);
```

### People In Space

```cs
var people_in_space = await OpenNotify.GetPeopleInSpace();
Console.WriteLine($"There are {people_in_space?.Number} people in space right now.");
var people = people_in_space
 ?.People
 ?.Select(p => $"Craft: {p.Craft}, Name: {p.Name}");
Console.WriteLine("People who are in space:");
Console.WriteLine(string.Join("\n", people));
```

</details>
<details>
<summary>JavaScript/TypeScript</summary>

### ISS Location

```js
const OpenNotify = require("OpenNotify");
const iss_location = await OpenNotify.getISSLocation();
// print iss location
console.log(
  "ISS location:\n" +
    `latitude: ${iss_location.latitude}\n` +
    `longitude: ${iss_location.longitude}`
);
```

### People In Space

```js
const OpenNotify = require("OpenNotify");
const peopleInSpace = await OpenNotify.getPeopleInSpace();
// print people in space
console.log("There are", peopleInSpace.number, "people in space right now:");
for (const { name, craft } of peopleInSpace.people) {
  console.log(name, "in", craft);
}
```

</details>

## References

[Open Notify Website](http://open-notify.org/)

[Official API documentation](http://open-notify.org/Open-Notify-API/)

## License

[MIT](https://github.com/iArmanKarimi/Open-Notify-API-clients/blob/main/LICENSE)

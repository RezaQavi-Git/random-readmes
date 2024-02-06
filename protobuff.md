# Protocol buffers

It’s like JSON, except it’s smaller and faster.

Protocol buffers provide a serialization format for packets of typed, structured data that are up to a few megabytes in size. The format is suitable for both ephemeral network traffic and long-term data storage. Protocol buffers can be extended with new information without invalidating existing data or requiring code to be updated.

Protocol buffers allow for the seamless support of changes, including the addition of new fields and the deletion of existing fields, to any protocol buffer without breaking existing services.

Protocol buffers are ideal for any situation in which you need to serialize structured, record-like, typed data in a language-neutral, platform-neutral, extensible manner. They are most often used for defining communications protocols (together with gRPC) and for data storage.

It’s standard for software products to be backward compatible, but it is less common for them to be forward compatible. As long as you follow some simple practices when updating .proto definitions, old code will read new messages without issues, ignoring any newly added fields. To the old code, fields that were deleted will have their default value, and deleted repeated fields will be empty.
New code will also transparently read old messages. New fields will not be present in old messages; in these cases protocol buffers provide a reasonable default value.

## Some of the advantages of using protocol buffers

- Compact data storage
- Fast parsing
- Availability in many programming languages
- Optimized functionality through automatically-generated classes
- Cross-language Compatibility
- Cross-project Support

## When are Protocol Buffers not a Good Fit?

- Protocol buffers tend to assume that entire messages can be loaded into memory at once and are not larger than an object graph.
- When protocol buffers are serialized, the same data can have many different binary serializations. You cannot compare two messages for equality without fully parsing them.
- Messages are not compressed.
- Protocol buffer messages are less than maximally efficient in both size and speed for many scientific and engineering uses that involve large, multi-dimensional arrays of floating point numbers. For these applications, FITS and similar formats have less overhead.
- Protocol buffers are not well supported in non-object-oriented languages popular in scientific computing
- Protocol buffer messages don’t inherently self-describe their data
- Protocol buffers are not a formal standard of any organization.

## How do Protocol Buffers Work?

Follow this link: [Link](https://protobuf.dev/overview/#work)

## Protocol Buffers Definition Syntax

A field can also be of:

- A message type, so that you can nest parts of the definition, such as for repeating sets of data.
- An enum type, so you can specify a set of values to choose from.
- A oneof type, which you can use when a message has many optional fields and at most one field will be set at the same time.
- A map type, to add key-value pairs to your definition.

There are some things to keep in mind when setting field names:

- It can sometimes be difficult, or even impossible, to change field names after they’ve been used in production.
- Field names cannot contain dashes
- Use pluralized names for repeated fields.

After assigning a name to the field, you assign a field number. Field numbers cannot be repurposed or reused. If you delete a field, you should reserve its field number to prevent someone from accidentally reusing the number.

## Unknown Fields

- Any
- Oneof

  - If you have a message with many fields and where at most one field will be set at the same time, you can enforce this behavior and save memory by using the oneof feature.

  - Oneof fields are like regular fields except all the fields in a oneof share memory, and at most one field can be set at the same time. Setting any member of the oneof automatically clears all the other members. You can check which value in a oneof is set (if any) using a special case() or WhichOneof() method, depending on your chosen language. Note that if multiple values are set, the last set value as determined by the order in the proto will overwrite all previous ones.

- Maps
- Packages

## Specifying Field Labels

Message fields can be one of the following:

- optional: An optional field is in one of two possible states:

- the field is set, and contains a value that was explicitly set or parsed from the wire. It will be serialized to the wire.
- the field is unset, and will return the default value. It will not be serialized to the wire.
  You can check to see if the value was explicitly set.

- repeated: this field type can be repeated zero or more times in a well-formed message. The order of the repeated values will be preserved.

- map: this is a paired key/value field type. See Maps for more on this field type.

## Default Values

When a message is parsed, if the encoded message does not contain a particular implicit presence element, accessing the corresponding field in the parsed object returns the default value for that field. These defaults are type-specific:

- For strings, the default value is the empty string.
- For bytes, the default value is empty bytes.
- For bools, the default value is false.
- For numeric types, the default value is zero. For float and double types, -0.0 and 0.0 are treated as equivalent, and will round-trip.
- For enums, the default value is the first defined enum value, which must be 0.
- For message fields, the field is not set. Its exact value is language-dependent.

## Reserved Values

If you update an enum type by entirely removing an enum entry, or commenting it out, future users can reuse the numeric value when making their own updates to the type.

One way to make sure this doesn’t happen is to specify that the numeric values (and/or names, which can also cause issues for JSON serialization) of your deleted entries are reserved. The protocol buffer compiler will complain if any future users try to use these identifiers. You can specify that your reserved numeric value range goes up to the maximum possible value using the max keyword.

```proto
enum Foo {
  reserved 2, 15, 9 to 11, 40 to max;
  reserved "FOO", "BAR";
}
```

## Proto Best Practices

- Don’t Re-use a Tag Number
- Do Reserve Tag Numbers for Deleted Fields
- Do Reserve Numbers for Deleted Enum Values
- Don’t Change the Type of a Field
- Don’t Add a Required Field
- Don’t Make a Message with Lots of Fields
- Do Include an Unspecified Value in an Enum
- Don’t Use C/C++ Macro Constants for Enum Values
- Do Use Well-Known Types and Common Types

  - Well-Known Types

    - duration is a signed, fixed-length span of time (for example, 42s).
    - timestamp is a point in time independent of any time zone or calendar (for example, 2017-01-15T01:30:15.01Z).
    - field_mask is a set of symbolic field paths (for example, f.b.d).

  - Common Types
    - Duration is a signed, fixed-length span of time, such as 42s.
    - Timestamp is a point in time independent of any time zone or calendar, such as 2017-01-15T01:30:15.01Z.
    - interval is a time interval independent of time zone or calendar (for example, 2017-01-15T01:30:15.01Z - 2017-01-16T02:30:15.01Z).
    - date is a whole calendar date (for example, 2005-09-19).
    - dayofweek is a day of week (for example, Monday).
    - timeofday is a time of day (for example, 10:42:23).
    - latlng is a latitude/longitude pair (for example, 37.386051 latitude and -122.083855 longitude).
    - money is an amount of money with its currency type (for example, 42 USD).
    - postal_address is a postal address (for example, 1600 Amphitheatre Parkway Mountain View, CA 94043 USA).
    - color is a color in the RGBA color space.
    - month is a month of year (for example, April).
  - Do Define Widely-used Message Types in Separate Files
  - Don’t Change the Default Value of a Field
  - Don’t Go from Repeated to Scalar

## Updating A Message Type

- Don’t change the field numbers for any existing fields. “Changing” the field number is equivalent to deleting the field and adding a new field with the same type.
- Fields can be removed, as long as the field number is not used again in your updated message type. You may want to rename the field instead, perhaps adding the prefix “OBSOLETE\_”, or make the field number reserved, so that future users of your .proto can’t accidentally reuse the number.
- int32, uint32, int64, uint64, and bool are all compatible – this means you can change a field from one of these types to another without breaking forwards- or backwards-compatibility.
- sint32 and sint64 are compatible with each other but are not compatible with the other integer types.
- string and bytes are compatible as long as the bytes are valid UTF-8.
- fixed32 is compatible with sfixed32, and fixed64 with sfixed64.
- For string, bytes, and message fields, optional is compatible with repeated.
- Changing a field between a map<K, V> and the corresponding repeated message field is binary compatible

# References

[protobuf.dev](https://protobuf.dev/overview/)

Working with QiTypes using .NET

-------------------------------


When working in .NET, use the QiTypeBuilder to create QiTypes. The QiTypeBuilder eliminates 
potential errors that can occur when working with QiTypes manually.

There are several ways to work with the builder. The most convenient is to use the static 
methods, as shown here:

::

  public enum State
  {
      Ok,
      Warning,
      Alarm
  }

  public class Simple
  {
      [QiMember(IsKey = true, Order = 0)]
      public DateTime Time { get; set; }
      public State State { get; set; }
      public Double Measurement { get; set; }
  }

  QiType simpleType = QiTypeBuilder.CreateQiType<Simple>();
  simpleType.Id = "Simple";
  simpleType.Name = "Simple";
  simpleType.Description = "Basic sample type";


QiTypeBuilder recognizes the ``System.ComponentModel.DataAnnotations.KeyAttribute`` and 
its own ``OSIsoft.Qi.QiMemberAttribute``. When using the QiMemberAttribute to specify 
the Primary Index, set the IsKey to true.

The type is created with the following parameters. QiTypeBuilder automatically generates 
unique identifiers. Note that the following table contains only a partial list of fields.


+------------------+-------------------------+-------------+--------------------------------------+
| Field            | Values                                                                       |
+==================+=========================+=============+======================================+
| Id               | Simple                                                                       |
+------------------+-------------------------+-------------+--------------------------------------+
| Name             | Simple                                                                       |
+------------------+-------------------------+-------------+--------------------------------------+
| Description      | Basic sample type                                                            |
+------------------+-------------------------+-------------+--------------------------------------+
| Properties       | Count = 3                                                                    |
+------------------+-------------------------+-------------+--------------------------------------+
|   [0]            | Id                      | Time                                               |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Name                    | Time                                               |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Description             | null                                               |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Order                   | 0                                                  |
+                  +-------------------------+-------------+--------------------------------------+
|                  | IsKey                   | true                                               |
+                  +-------------------------+-------------+--------------------------------------+
|                  | QiType                  | Id          | c48bfdf5-a271-384b-bf13-bd21d931c1bf |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Name        | DateTime                             |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Description | null                                 |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Properties  | null                                 |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Value                   | null                                               |
+------------------+-------------------------+-------------+--------------------------------------+
|   [1]            | Id                      | State                                              |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Name                    | State                                              |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Description             | null                                               |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Order                   | 0                                                  |
+                  +-------------------------+-------------+--------------------------------------+
|                  | IsKey                   | false                                              |
+                  +-------------------------+-------------+--------------------------------------+
|                  | QiType                  | Id          | 02728a4f-4a2d-3588-b669-e08f19c35fe5 |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Name        | State                                |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Description | null                                 |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Properties  | Count = 3                            |
+                  +                         +-------------+-------------------+------------------+
|                  |                         | [0]         | Id                | "Ok"             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Name              | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Description       | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Order             | 0                |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | QiType            | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Value             | 0                |
+                  +                         +-------------+-------------------+------------------+
|                  |                         | [1]         | Id                | "Warning"        |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Name              | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Description       | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Order             | 0                |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | QiType            | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Value             | 1                |
+                  +                         +-------------+-------------------+------------------+
|                  |                         | [2]         | Id                | "Alarm"          |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Name              | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Description       | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Order             | 0                |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | QiType            | null             |
+                  +                         +             +-------------------+------------------+
|                  |                         |             | Value             | 2                |
+                  +-------------------------+-------------+-------------------+------------------+
|                  | Value                   | null                                               |
+------------------+-------------------------+-------------+-------------------+------------------+
|   [2]            | Id                      | Measurement                                        |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Name                    | Measurement                                        |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Description             | null                                               |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Order                   | 0                                                  |
+                  +-------------------------+-------------+--------------------------------------+
|                  | IsKey                   | false                                              |
+                  +-------------------------+-------------+--------------------------------------+
|                  | QiType                  | Id          | 0f4f147f-4369-3388-8e4b-71e20c96f9ad |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Name        | Double                               |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Description | null                                 |
+                  +                         +-------------+--------------------------------------+
|                  |                         | Properties  | null                                 |
+                  +-------------------------+-------------+--------------------------------------+
|                  | Value                   | null                                               |
+------------------+-------------------------+-------------+--------------------------------------+


The QiTypeBuilder also supports derived types. Note that you need not add the base types to 
Qi before using QiTypeBuilder.


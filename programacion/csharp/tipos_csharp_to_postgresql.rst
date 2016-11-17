.. _reference-programacion-csharp-tipos_csharp_to_postgresql:

######################
Tipos C# to PostgreSQL
######################

Fuentes
*******

* http://stackoverflow.com/questions/845458/postgresql-and-c-sharp-datatypes
* http://npgsql.projects.pgfoundry.org/docs/manual/UserManual.html

---------------------

==============  ==============  ====================    =================
Postgresql      NpgsqlDbType    System.DbType Enum      .Net System Type
==============  ==============  ====================    =================
int8            Bigint          Int64                   Int64
bool            Boolean         Boolean                 Boolean
bytea           Bytea           Binary                  Byte[]
date            Date            Date                    DateTime
float8          Double          Double                  Double
int4            Integer         Int32                   Int32
money           Money           Decimal                 Decimal
numeric         Numeric         Decimal                 Decimal
float4          Real            Single                  Single
int2            Smallint        Int16                   Int16
text            Text            String                  String
time            Time            Time                    DateTime
timetz          Time            Time                    DateTime
timestamp       Timestamp       DateTime                DateTime
timestamptz     TimestampTZ     DateTime                DateTime
interval        Interval        Object                  TimeSpan
varchar         Varchar         String                  String
inet            Inet            Object                  IPAddress
bit             Bit             Boolean                 Boolean
uuid            Uuid            Guid                    Guid
array           Array           Object                  Array
==============  ==============  ====================    =================

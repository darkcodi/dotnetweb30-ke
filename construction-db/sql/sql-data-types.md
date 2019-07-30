# SQL data types

### String data types

| Data type | Description | Max size | Storage |
| :--- | :--- | :--- | :--- |
| char\(n\) | Fixed width character string | 8,000 characters | Defined width |
| varchar\(n\) | Variable width character string | 8,000 characters | 2 bytes + number of chars |
| varchar\(max\) | Variable width character string | 1,073,741,824 characters | 2 bytes + number of chars |
| text | Variable width character string | 2GB of text data | 4 bytes + number of chars |
| nchar | Fixed width Unicode string | 4,000 characters | Defined width x 2 |
| nvarchar | Variable width Unicode string | 4,000 characters |  |
| nvarchar\(max\) | Variable width Unicode string | 536,870,912 characters |  |
| ntext | Variable width Unicode string | 2GB of text data |  |
| binary\(n\) | Fixed width binary string | 8,000 bytes |  |
| varbinary | Variable width binary string | 8,000 bytes |  |
| varbinary\(max\) | Variable width binary string | 2GB |  |
| image | Variable width binary string | 2GB |  |

### Numeric data types

<table>
  <thead>
    <tr>
      <th style="text-align:left">Data type</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Storage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">bit</td>
      <td style="text-align:left">Integer that can be 0, 1, or NULL</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">tinyint</td>
      <td style="text-align:left">Allows whole numbers from 0 to 255</td>
      <td style="text-align:left">1 byte</td>
    </tr>
    <tr>
      <td style="text-align:left">smallint</td>
      <td style="text-align:left">Allows whole numbers between -32,768 and 32,767</td>
      <td style="text-align:left">2 bytes</td>
    </tr>
    <tr>
      <td style="text-align:left">int</td>
      <td style="text-align:left">Allows whole numbers between -2,147,483,648 and 2,147,483,647</td>
      <td
      style="text-align:left">4 bytes</td>
    </tr>
    <tr>
      <td style="text-align:left">bigint</td>
      <td style="text-align:left">Allows whole numbers between -9,223,372,036,854,775,808 and 9,223,372,036,854,775,807</td>
      <td
      style="text-align:left">8 bytes</td>
    </tr>
    <tr>
      <td style="text-align:left">decimal(p,s)</td>
      <td style="text-align:left">
        <p>Fixed precision and scale numbers.</p>
        <p>Allows numbers from -10^38 +1 to 10^38 &#x2013;1.</p>
      </td>
      <td style="text-align:left">5-17 bytes</td>
    </tr>
    <tr>
      <td style="text-align:left">numeric(p,s)</td>
      <td style="text-align:left">Decimal and numeric are synonyms and can be used interchangeably.</td>
      <td
      style="text-align:left">5-17 bytes</td>
    </tr>
    <tr>
      <td style="text-align:left">smallmoney</td>
      <td style="text-align:left">Monetary data from -214,748.3648 to 214,748.3647</td>
      <td style="text-align:left">4 bytes</td>
    </tr>
    <tr>
      <td style="text-align:left">money</td>
      <td style="text-align:left">Monetary data from -922,337,203,685,477.5808 to 922,337,203,685,477.5807</td>
      <td
      style="text-align:left">8 bytes</td>
    </tr>
    <tr>
      <td style="text-align:left">float(n)</td>
      <td style="text-align:left">Floating precision number data from -1.79E+308 to 1.79E+308.</td>
      <td style="text-align:left">4 or 8 bytes</td>
    </tr>
    <tr>
      <td style="text-align:left">real</td>
      <td style="text-align:left">Floating precision number data from -3.40E+38 to 3.40E+38</td>
      <td style="text-align:left">4 bytes</td>
    </tr>
  </tbody>
</table>### Date and Time data types

| Data type | Description | Storage |
| :--- | :--- | :--- |
| datetime | From January 1, 1753 to December 31, 9999 with an accuracy of 3.33 milliseconds | 8 bytes |
| datetime2 | From January 1, 0001 to December 31, 9999 with an accuracy of 100 nanoseconds | 6-8 bytes |
| smalldatetime | From January 1, 1900 to June 6, 2079 with an accuracy of 1 minute | 4 bytes |
| date | Store a date only. From January 1, 0001 to December 31, 9999 | 3 bytes |
| time | Store a time only to an accuracy of 100 nanoseconds | 3-5 bytes |
| datetimeoffset | The same as datetime2 with the addition of a time zone offset | 8-10 bytes |
| timestamp | Stores a unique number that gets updated every time a row gets created or modified. The timestamp value is based upon an internal clock and does not correspond to real time. |  |

### Other data types

| Data type | Description |
| :--- | :--- |
| sql\_variant | Stores up to 8,000 bytes of data of various data types, except text, ntext, and timestamp |
| uniqueidentifier | Stores a globally unique identifier \(GUID\) |
| xml | Stores XML formatted data. Maximum 2GB |
| cursor | Stores a reference to a cursor used for database operations |
| table | Stores a result-set for later processing |


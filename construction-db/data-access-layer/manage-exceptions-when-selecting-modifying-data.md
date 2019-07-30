# Manage exceptions when selecting, modifying data

The `SqlException` has a **Number** property that you can check.

```csharp
catch (SqlException e)
{
   switch (e.Number)
   {
      case 2601: // duplicate error
         // Do something.
         break;
      default:
         throw;
   }
 }
```

The following table describes the possible values for this property:

| Source of Error | SqlError.Number | SqlException has inner Win32Exception \(beginning with.NET Framework 4.5\) |
| :--- | :--- | :--- |
| Error from server | Server error code   This number corresponds to an entry in the `master.dbo.sysmessages` table. | No |
| Connection timeout | -2 | Yes \(Number = 258\) |
| Communication error \(non-LocalDB\) | Win32 error code | Yes \(Number = Win32 error code\) |
| Communication error \(LocalDB\) | Win32 error code | No |
| Encryption capability mismatch | 20 | No |
| Failed to start LocalDB | Win32 error code | No |
| Read-only routing failure / Server had severe error processing query | 0 | No |


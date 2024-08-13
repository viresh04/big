```py
cd Documents/
```
```py
 nano viresh.txt 
```
```py
mapper code
```
```py
viresh.txt | python mapper.py 
```
```py
nano reducer.py
```
```py
reducer code
```
```py
cat viresh.txt | python mapper.py  | sort -k1,1 | python reducer.py 
```
```py
start-all.sh
```
```py
jps
```
```py
hdfs dfs -mkdir /vd
```
```py
hdfs dfs -copyFromLocal /home/hduser/Documents/viresh.txt  /vd
```
```py
hdfs dfs -ls /
```
```py
chmod 777 mapper.py reducer.py 
```
```py
ls -l
```
```py
hadoop jar /home/hduser/Documents/hadoop-streaming-2.7.3.jar \
```
```py
-input /vd/viresh.txt \
```
```py
-output /vd/output \
```
```py
-mapper /home/hduser/Documents/mapper.py \	
```
```py
-reducer /home/hduser/Documents/reducer.py 
```

# 1.Map Reduce program to read a text file count the number of occurrences of the words.

# 1. mapper.py

-mapper.py

```py
#!/usr/bin/env python
import sys
for line in sys.stdin:
    line = line.strip()
    words = line.split()
    for word in words:
        print '%s\t%s' % (word, 1)

```

# 1. reducer.py

- reducer.py

```py
#!/usr/bin/env python
from operator import itemgetter
import sys
current_word = None
current_count = 0
word = None
for line in sys.stdin:
    line = line.strip()
    word, count = line.split('\t', 1)
    try:
        count = int(count)
    except ValueError:
        continue
    if current_word == word:
        current_count += count
    else:
        if current_word:
            print '%s\t%s' % (current_word, current_count)
        current_count = count
        current_word = word
if current_word == word:
    print '%s\t%s' % (current_word, current_count)

```
# 
# 2: Map Reduce program to display the number of transactions and sales count from shopping cart.

# 2. mapper.py

```py
import string
import fileinput
for line in fileinput.input():
    data = line.strip().split("\t")
    if len(data) == 6:
        date, time, location, item, cost, payment = data
        print "{0}\t{1}".format(location, cost)
```

# 2. reducer.py

```py
import fileinput
transactions_count = 0
sales_total = 0
for line in fileinput.input():
    data = line.strip().split("\t")    
    if len(data) != 2:
        continue
    current_key, current_value = data
    transactions_count += 1
    sales_total += float(current_value)
print transactions_count, "\t", sales_total

```

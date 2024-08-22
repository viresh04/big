# 1st and 2nd prg
#2nd prg viresh.txt
```py
2012-07-16     15:43	 Bangalore	Men's Clothing	208.97	Visa	
2012-07-18     20:15	 Mumbai  	Electronics	1005.20	cash
```
```py
cd Documents
sudo mkdir termwork1
cd terwork1
sudo nano word.txt
cat word.txt
sudo nano mapper.py
cat mapper.py
ls
cat word.txt | python mapper.py
sudo nano reduer.py
cat reducer.py
cat word.txt | python mapper.py | python reducer.py
jps
start-all.sh
jps
hdfs dfs -mkdir /tw1
hdfs dfs -ls/
hdfs dfs -copyFromLocal /home/hduser/Documents/twerwork1/word.txt/tw1
hdfs dfs -ls/tw1
sudo chmod 777 mapper.py reducer.py
ls -l
hadoop jar /home/hduser/docments/hadoop-streaming 2.7.3 jar \
-input /tw1/word.txt \
-output /tw1/123 \
-mapper /home/hduser/Documents/termwork1/mapper.py \
-reducer /home/hdusre/Documents/termwork1/redcer.py

hdfs dfs -cat/tw1/123/part-00000

```
```py
cd Documents/
```
```py
sudo mkdir vmd
```
```py
cd vmd
```
```py
sudo nano age.txt
```
```py
cat age.txt
```
```py
ls
```
```py
 sudo nano mapper1.py
```
```py
ls
```
```py
cat  mapper1.py
```
```py
cat age.txt |python mapper1.py 
```
```py
sudo nano reducer1.py
```
```py
cat reducer1.py
```
```py
ls
```
```py
cat viresh.txt | python mapper1.py | python reducer1.py 
```
```py
start-all.sh
```
```py
jps
```
```py
#safe mode
hdfs dfsadmin –safemode leave
```
```py
hdfs dfs -mkdir /ui
```
```py
hdfs dfs -copyFromLocal /home/hduser/Documents/vmd/age.txt /ui
```
```py
hdfs dfs -ls /
or
 hdfs dfs -ls /ui
```
```py
chmod 777 mapper1.py reducer1.py 
```
```py
ls -l
```
```py
hadoop jar /home/hduser/Documents/hadoop-streaming-2.7.3.jar \
   or
hadoop jar /home/hduser/Downloads/hadoop-streaming-2.7.3.jar \
```
```py
-input /ui/age.csv \
```
```py
-output /ui/12345 \
```
```py
-mapper /home/hduser/Documents/vmd/mapper1.py \
```
```py
-reducer /home/hduser/Documents/vmd/reducer1.py
```
```py
 hdfs dfs -cat /ui/12345/part-00000
```
```py
localhost:50070/
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
```py
hdfs dfsadmin -safemode leave
```

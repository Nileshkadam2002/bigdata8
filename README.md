# bigdata8
ass8
Ass 8
Integrate UDFs to enhance the functionality of Pig scripts. (Write hadoop
code to concatenation two string )

Step 1: Open Java Eclipse -> Make New Project->(PigAss7) Add External Libarary->pig , hadoop
,hadoop 0.20_map_reduce->finish
Step 2: Add class in project -> (Ass8Demo) -> Write below code (Create the UDF)
import org.apache.pig.EvalFunc;
import org.apache.pig.data.Tuple;
import org.apache.pig.data.DataByteArray;
public class ConcatStrings extends EvalFunc<DataByteArray> {
@Override
public DataByteArray exec(Tuple input) {
if (input == null || input.size() < 2)
return null;
try {
String str1 = (String) input.get(0);
String str2 = (String) input.get(1);
return new DataByteArray((str1 +
str2).getBytes());
} catch (Exception e) {
return null;
}
}
}
Step 3: Export java project in to jar file ->Ass8Demo.jar
Step 4: Open terminal create strdata.txt file using following command
vi strdata.txt
hi,hello
good,morning
welcome,RCPET’s IMRD
Step 5: Open terminal to create pig file using following command.
vi strcat.pig
Write following code in file
REGISTER /home/cloudera/Ass8Demo.jar
DEFINE ConcatStrings ConcatStrings();
data=LOAD ‘/home/cloudera/strdata.txt’ Using PigStorage(‘,’)
as (str1:chararray,str2:chararray);
result = FOREACH data GENERATE ConcatStrings(str1,str2);

DUMP result;
Step 6: Run Pig script
pig –x local strcat.pig

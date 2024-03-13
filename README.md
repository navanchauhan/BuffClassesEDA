# CU Boulder Grade Data

## Steps to Update Database:

1. Fetch Latest Data from [CU's ODA Website](https://www.colorado.edu/oda/student-data/courses) (Over Time Reports -> Grades -> Grade distributions) (should be a file named gradesall on Google Drive)
2. Export `Data` sheet as a CSV file. Say `data2.csv`
3. Using `sqlite3` import the CSV file.

```
$ sqlite3 newdb.sqlite
```

```
sqlite> CREATE TABLE IF NOT EXISTS "raw_data" (
"YearTerm" INTEGER,
  "CrsPBADept" TEXT,
  "CrsPBAColl" TEXT,
  "CrsPBADiv" TEXT,
  "Subject" TEXT,
  "Course" INTEGER,
  "CourseTitle" TEXT,
  "Level" TEXT,
  "CrsLvlNum" TEXT,
  "Activity_Type" TEXT,
  "Instruction_Mode" TEXT,
  "Hours" REAL,
  "N_EOT" INTEGER,
  "N_ENROLL" INTEGER,
  "N_GRADE" REAL,
  "PCT_GRADE" TEXT,
  "AVG_GRD" REAL,
  "PCT_A" TEXT,
  "PCT_B" TEXT,
  "PCT_C" TEXT,
  "PCT_D" TEXT,
  "PCT_F" TEXT,
  "PCT_C_MINUS_OR_BELOW" TEXT,
  "PCT_DF" TEXT,
  "PCT_DFW" TEXT,
  "PCT_WDRAW" TEXT,
  "PCT_INCOMP" TEXT,
  "N_PASS" INTEGER,
  "N_NOCRED" INTEGER,
  "N_INCOMP" INTEGER,
  "RAP" INTEGER,
  "Honors" INTEGER,
  "insname1" TEXT,
  "insgrp1" TEXT,
  "insttl1" TEXT,
  "insname2" TEXT,
  "insgrp2" TEXT,
  "insttl2" TEXT,
  "insname3" TEXT,
  "insgrp3" TEXT,
  "insttl3" TEXT,
  "Section" TEXT,
  "NComb" INTEGER,
  "Subject_Label" TEXT
);
sqlite> .mode csv
sqlite> .import data2.csv raw_data
sqlite> DELETE from raw_data where YearTerm < 20161;
sqlite> VACUUM;
```

Now, you can replace the database with the latest version:

```
$ mv newdb.sqlite grades.sqlite
```

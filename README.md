oracle_pdb_ass_II_20251SEN133_Harerimana
Oracle Progeble_Databse 

* ## Overview of Tasks 
     This assignment demonstrates practical understanding of 
     Oracle PDB creation/deletion, user management, and Oracle Enterprise Manager.

* ## Oracle Environment Used 
     Database Edition: Oracle Database 21c Express Edition (XE),Operating System: Windows 11 , Management Tool:  SQL*Plus & Oracle Enterprise Manager Database Express 21c

* ## Explanation of Each Task Done 

 ##### Task 1: Pluggable Database (PDB) Creation & User Management
  I created a new Pluggable Database named * Ha_pdb_20251SEN133 * insidethe Oracle container database,opened it,and then created a user called * Harerimana_plsqlauca_20251SEN133 * inside that PDB with basic privileges 
READ,WRITE 

*  ##### Commands Used: 
-- Creation of database
  ```   
  CREATE PLUGGABLE DATABASE HA_PDB_20251SEN133 ADMIN USER pdb_admin IDENTIFIED BY Pdb123
  FILE_NAME_CONVERT = ('C:\ORACLE\ORA\ORADATA\XE\PDBSEED\', 'C:\ORACLE\ORA\ORADATA\XE\HA_PDB_20251SEN133\');

<img width="1918" height="150" alt="Screenshot 2026-10-06 170252" src="https://github.com/user-attachments/assets/ccef2d82-170f-4466-8d6c-50b6b5f67030" />
```
--- Open it to use it
```  
  ALTER PLUGGABLE DATABASE HA_PDB_20251SEN133 OPEN;
  ALTER SESSION SET CONTAINER = HA_PDB_20251SEN133;
```
creation of user and grant permissions
```
CREATE USER harerimana_plsqlauca_20251SEN133 IDENTIFIED BY Pdb123;
  GRANT CONNECT, RESOURCE TO harerimana_plsqlauca_20251SEN133;
```
* #### Task 2 – Create and Delete a PDB 
     I created a temporary PDB named ` Ha_to_delete_pdb_20251SEN133 `,
     verified it appeared in the PDB list, closed it, 
      dropped it completely including its datafiles, and  confirmed it was gone.
 
* ###### Commands Used 
  -- creation

``` sql
  CREATE PLUGGABLE DATABASE Ha_to_delete_pdb_20251SEN133
  ADMIN USER temp_admin IDENTIFIED BY Temp123
  FILE_NAME_CONVERT = ('C:\ORACLE\ORA\ORADATA\XE\PDBSEED\', 'C:\ORACLE\ORA\ORADATA\XE\Ha_to_delete_pdb_20251SEN133\');
```
--- Drop
 ```   
  DROP PLUGGABLE DATABASE Ha_to_delete_pdb_20251SEN133 INCLUDING DATAFILES;
```
* #### Task 3: OEM Dashboard Monitoring *

I opened the Oracle Enterprise Manager web interface 
at * https://localhost:5500/em *, 
logged in as * username : SYSTEM and Pass : 123 *, and confirmed that 
the dashboard correctly displays my database environment including the PDB 
created in Task 1 and my logged-in username.

* ## Challenges and Solutions *

 Insufficient Privileges (ORA-01031):
> Encountered when attempting to open the PDB without administrative rights.

Solution:
> Connected to SQL*Plus using CONNECT / AS SYSDBA.

* File Path Syntax Error (ORA-65005)*
  Unix-style forward slashes (/pdbseed/) failed on Windows. 

Solution: 
> Replaced with correct Windows absolute paths containing backslashes (C:\ORACLE\...).

Container Name Login Error in OEM: 
Mistakenly entered SYSDBA into the container name field instead of leaving it blank. 

Solution: 
> Left the container field default/blank while logging in with system.


** Required Submission Details Block **
. Repository Link: https://github.com/jearclaude1/oracle_pdb_ass_II_20251SEN133_Harerimana.git
. PDB Name Created: HA_PDB_20251SEN133
. Issues Encountered: No

* ## Integrity statement *
 All database configurations, commands, testing, and documentation
 presented in this repository were independently performed, verified,
 and structured by me using  my local Oracle Database environment.

## thx 

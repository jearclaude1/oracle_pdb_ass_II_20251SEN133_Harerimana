oracle_pdb_ass_II_20251SEN133_Harerimana
Oracle Progeble_Databse 

# Overview of Tasks
Oracle Database Pluggable Database (PDB) creation, management, cleanup, and monitoring via Oracle Enterprise Manager (OEM).

# Oracle Environment Used
* **Database Edition:** Oracle Database 21c Express Edition (XE)
* **Operating System :**  Windows 11 
* **Management Tool:** SQL*Plus & Oracle Enterprise Manager Database Express 21c

* ### Task 1: Pluggable Database (PDB) Creation & User Management
* **Commands Used:**
  ``` sql
  --  Creation of database 
  CREATE PLUGGABLE DATABASE HA_PDB_20251SEN133 ADMIN USER pdb_admin IDENTIFIED BY Pdb123
  FILE_NAME_CONVERT = ('C:\ORACLE\ORA\ORADATA\XE\PDBSEED\', 'C:\ORACLE\ORA\ORADATA\XE\HA_PDB_20251SEN133\');

<img width="1918" height="150" alt="Screenshot 2026-10-06 170252" src="https://github.com/user-attachments/assets/ccef2d82-170f-4466-8d6c-50b6b5f67030" />

  -- Open it to use it 
  ALTER PLUGGABLE DATABASE HA_PDB_20251SEN133 OPEN;
  ALTER SESSION SET CONTAINER = HA_PDB_20251SEN133;

  <img width="1778" height="92" alt="Screenshot 2026-10-06 181048" src="https://github.com/user-attachments/assets/323c38cb-c945-47df-a927-6404e6696e26" />

  -- creation of user and grant permissions 
  CREATE USER harerimana_plsqlauca_20251SEN133 IDENTIFIED BY Pdb123;
  GRANT CONNECT, RESOURCE TO harerimana_plsqlauca_20251SEN133;

  <img width="1913" height="186" alt="image" src="https://github.com/user-attachments/assets/fc9811e5-a00d-4de4-8a2a-963169981901" />
  <img width="1852" height="148" alt="image" src="https://github.com/user-attachments/assets/3639ed46-aeaa-4fbf-804c-50675408a0c6" />

  Task 2: PDB Cleanup & Temporary Database Management
  Objective: creating and dropping temporary pluggable databases to manage storage and resources.
  Commands Used:
` sql
 -- creation
  CREATE PLUGGABLE DATABASE Ha_to_delete_pdb_20251SEN133
  ADMIN USER temp_admin IDENTIFIED BY Temp123
  FILE_NAME_CONVERT = ('C:\ORACLE\ORA\ORADATA\XE\PDBSEED\', 'C:\ORACLE\ORA\ORADATA\XE\Ha_to_delete_pdb_20251SEN133\');

<img width="1866" height="156" alt="image" src="https://github.com/user-attachments/assets/7b4a5262-47ed-42c5-9b2d-35dbd5027fe5" />
  <img width="1918" height="280" alt="image" src="https://github.com/user-attachments/assets/e5638a3c-f9cb-4a46-ae47-e0275a42b5ec" />
 
 -- Drop
`` sql
  DROP PLUGGABLE DATABASE Ha_to_delete_pdb_20251SEN133 INCLUDING DATAFILES;
  <img width="1913" height="343" alt="image" src="https://github.com/user-attachments/assets/381a4e66-35a7-4d31-8482-fd164930b9e1" />

  Task 3: Oracle Enterprise Manager
  Objective: Verify and monitor the Oracle database environment and active pluggable databases through OEM Express.
  Steps Taken: Checked the HTTPS port (5500), bypassed the self-signed SSL warning "  is not secured warning ", logged in as system

  <img width="1918" height="988" alt="Screenshot 2026-10-06 173704" src="https://github.com/user-attachments/assets/a9a8cdab-ad37-46f4-8182-48ad3cfcab13" />
  <img width="1918" height="1017" alt="image" src="https://github.com/user-attachments/assets/150e2731-3ecf-42ec-b977-a1eb0714cdc3" />

Challenges and Solutions
Insufficient Privileges (ORA-01031): Encountered when attempting to open the PDB without administrative rights.
<img width="1918" height="798" alt="Screenshot 2026-10-06 171135" src="https://github.com/user-attachments/assets/ccd33698-c27a-4020-b468-9984c536eecd" />
Solution: Connected to SQL*Plus using CONNECT / AS SYSDBA.
<img width="1918" height="317" alt="Screenshot 2026-10-06 163946" src="https://github.com/user-attachments/assets/b8c4acfc-ed5a-4695-a9f9-8ecc22495769" />

File Path Syntax Error (ORA-65005): 
Unix-style forward slashes (/pdbseed/) failed on Windows. Solution: 
-- Replaced with correct Windows absolute paths containing backslashes (C:\ORACLE\...).

Container Name Login Error in OEM: 
Mistakenly entered SYSDBA into the container name field instead of leaving it blank. 
Solution: Left the container field default/blank while logging in with system.


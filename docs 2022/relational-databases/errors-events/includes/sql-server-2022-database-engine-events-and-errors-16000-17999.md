---
author: rwestMSFT
ms.author: randolphwest
ms.date: 01/11/2024
ms.topic: include
---
| Error | Severity | Event logged | Description |
| :--- | :--- | :--- | :--- |
| 16001 | 16 | No | Data masking is not supported for the data type of column '%.\*ls'. |
| 16002 | 16 | No | Invalid data masking function in column '%.\*ls'. |
| 16003 | 16 | No | The data type of column '%.\*ls' does not support data masking function '%.\*ls'. |
| 16004 | 16 | No | Incorrect number of parameters for data masking function '%.\*ls' for column '%.\*ls'. |
| 16005 | 16 | No | Invalid argument for data masking function '%.\*ls' for column '%.\*ls'. |
| 16006 | 16 | No | Invalid data masking format for function '%.\*ls' in column '%.\*ls'. |
| 16007 | 16 | No | The column '%.\*ls' does not have a data masking function. |
| 16008 | 16 | No | Cannot add a masking function to a column that is encrypted. |
| 16009 | 16 | No | Cannot add a masking function to a column used as a sparse column set. |
| 16010 | 16 | No | External script cannot be executed on masked data columns. |
| 16011 | 16 | No | The data masking function for column '%.\*ls' is too long. |
| 16012 | 16 | No | The query accessed too many different databases. |
| 16013 | 16 | No | Cannot add a masking function to a column used in a key to a fulltext index. |
| 16014 | 16 | No | Failed to create fulltext index because key column '%.\*ls' has a masking function defined on it. |
| 16015 | 16 | No | The index on view '%.\*ls' cannot be created because the view is referencing table '%.\*ls' with masked columns. |
| 16016 | 16 | No | Cannot add a masking function to a column used in a sparse column set. |
| 16017 | 16 | No | The query used too many masked sources. |
| 16101 | 16 | No | Option '%.\*ls' is not supported for sensitivity classification. |
| 16102 | 16 | No | Object name specified '%.\*ls' is not valid. |
| 16103 | 16 | No | Sensitivity classification is not supported for the specified object. |
| 16104 | 16 | No | Sensitivity classification option '%.\*ls' was repeated. |
| 16105 | 16 | No | Option '%.\*ls' is too long (max %d chars). |
| 16106 | 16 | No | Option '%.\*ls' is empty. |
| 16107 | 16 | No | Schema '%.\*ls' was not found or you do not have permission to access it. |
| 16108 | 16 | No | Table '%.\*ls' was not found or you do not have permission to access it. |
| 16109 | 16 | No | Column '%.\*ls' was not found in table '%.\*ls' or you do not have permission to access it. |
| 16110 | 16 | No | Specification of database part of object name is not supported. |
| 16111 | 16 | No | Sensitivity classification operations cannot be used on computed column '%.\*ls'. |
| 16112 | 16 | No | Sensitivity classifications cannot be added to a history table directly. |
| 16113 | 16 | No | Sensitivity rank must not be provided as string. |
| 16114 | 16 | No | Sensitivity rank must be one of the following: NONE, LOW, MEDIUM, HIGH, CRITICAL. |
| 16115 | 16 | No | '%.\*ls' option's value must be provided as string. |
| 16116 | 16 | No | Object '%.\*ls' is not a table. |
| 16200 | 16 | No | The statement failed because 'APPROX_COUNT_DISTINCT' does not support DISTINCT \<column-name\> parameters. Consider using 'APPROX_COUNT_DISTINCT' without DISTINCT, or COUNT or COUNT_BIG with DISTINCT. |
| 16201 | 16 | No | The statement failed because '%.\*ls' does not support DISTINCT \<column-name\> parameters. |
| 16202 | 16 | No | Keyword or statement option '%.\*ls' is not supported on the '%.\*ls' platform. |
| 16203 | 15 | No | The option "INLINE=ON" is not valid for this function. Check the documentation for the constructs supported with INLINE option in a function. |
| 16204 | 15 | No | Invalid column ordinal provided for column %d. Column ordinal has to be greater than zero. |
| 16205 | 15 | No | Invalid read length provided in OPENROWSET query. Length has to be greater than zero. |
| 16206 | 15 | No | Only 'CELL_MAPPING' can be specified as a table-level JSON hint. |
| 16207 | 15 | No | Invalid PLAN PER VALUE hint definition. |
| 16208 | 15 | No | The function '%.\*ls' does not support %.\*ls. |
| 16209 | 15 | No | The PARTITION=ALL clause must be specified to enable XML compression for the table or index. |
| 16210 | 16 | No | Invalid xml compression setting for columnstore index '%.\*ls'. |
| 16211 | 15 | No | Cannot repeat window name in the WINDOW clause. |
| 16212 | 15 | No | The function '%.\*ls' expects parameter %.\*ls at position %d. |
| 16213 | 15 | No | All parameters of '%.\*ls' must be named. |
| 16310 | 16 | No | '%.\*ls' is not supported in this version of Azure SQL Edge. |
| 16401 | 16 | No | Page id not hosted by the current page server. |
| 16501 | 16 | No | %ls is not supported with this set of options. |
| 16502 | 16 | No | Cannot execute stored procedure '%ls'. The security check for the current user is failing. Only members of the sysadmin role can perform this operation. |
| 16503 | 16 | No | Cannot complete the sp_set_data_processed_limit stored procedure. Invalid type is specified. Valid values are: daily, weekly and monthly. |
| 16504 | 16 | No | Query is rejected because SQL Serverless budget limit for a period is exceeded. (Period = %s: Limit = %lu TB, Data processed = %lu TB) |
| 16505 | 16 | No | EXTERNAL FILE FORMAT '%ls' has FORMAT_TYPE = %ls which is not supported by CREATE EXTERNAL TABLE AS SELECT statement. |
| 16506 | 16 | No | The column name starting with '%.\*ls' is too long. The maximum length is %d characters. File: '%ls'. |
| 16507 | 16 | No | String or binary data would be truncated while reading column of type '%ls'. Check ANSI_WARNINGS option. File/External table name '%ls', column '%ls'. Truncated value: '%ls'. |
| 16508 | 16 | No | Error converting values NaN or Infinity to type '%ls'. NaN and Infinity are not supported. File/External table name '%ls', column '%ls', value '%ls'. Check ANSI_WARNINGS and ARITHABORT options. |
| 16509 | 16 | No | Arithmetic overflow error converting '%ls' to data type '%ls'. File/External table name '%ls', column '%ls', value '%ls'. Check ANSI_WARNINGS, ARITHABORT and NUMERIC_ROUNDABORT options. |
| 16510 | 16 | No | Persisting distributed query history into %ls table failed. Table does not exists or it is corrupted. |
| 16511 | 16 | No | Persisting distributed query history into %ls table failed. Command '%ls' failed. |
| 16512 | 16 | No | Resolving Delta logs on path '%ls' failed with error: There are null fields in file/schema resolution. |
| 16513 | 16 | No | Error reading external metadata. |
| 16514 | 16 | No | Resolving Delta logs on path '%ls' failed with error: Cannot parse json object from log folder. |
| 16515 | 16 | No | Resolving Delta logs on path '%ls' failed with error: Cannot find value of partitioning column '%.\*ls' in file '%ls'. |
| 16516 | 16 | No | Resolving Delta logs on path '%ls' failed with error: Wildcard in table path is not supported. |
| 16517 | 16 | No | Resolving Delta logs on path '%ls' failed with error: Could not the find expected number of log files. |
| 16518 | 16 | No | Resolving Delta logs on path '%ls' failed with error: Cannot parse field field '%ls' in json object. |
| 16519 | 16 | No | Resolving Delta logs on path '%ls' failed with error: Provider type '%.\*ls' is not supported. |
| 16520 | 16 | No | Resolving Delta logs on path '%ls' failed with error: Partitioning column '%.\*ls' not found in inferred or provided schema. |
| 16521 | 16 | No | Resolving Delta logs on path '%ls' failed with error: Schema inference failed to parse type '%ls'. |
| 16522 | 10 | No | %.\*ls input argument should be a OPENROWSET BULK query which uses external extraction. |
| 16523 | 16 | Yes | Execution service has shut down so performing distributed computation cannot be executed unless SQL is restarted |
| 16524 | 16 | No | Master Key for CosmosDb collection %ls was not specified. |
| 16525 | 17 | No | Failed to enqueue system background tasks during SQL server startup. |
| 16526 | 17 | No | Terminating the %ls system task because of unrecoverable exception. |
| 16527 | 16 | No | Type %ls of partition column %.\*ls is not supported for external tables. |
| 16528 | 16 | No | Operation '%ls %ls' failed. Retry the operation later. |
| 16529 | 16 | No | IO operation failed during processing '%ls' in file '%ls' with error : '%ls'. |
| 16530 | 16 | No | IO operation failed during processing file '%ls' with error : '%ls'. |
| 16531 | 16 | No | Budget limit cannot be changed. Condition that must be satisfied: daily limit \<= weekly limit \<= monthly limit. |
| 16532 | 16 | No | Cannot explicitly reference delimited text file columns by name unless OPENROWSET option HEADER_ROW is set to TRUE. |
| 16533 | 18 | No | Error classification failed due to internal error, please contact support. |
| 16534 | 16 | No | Cannot create or alter database. |
| 16535 | 16 | No | Cannot bulk load. The file "%ls" does not exist or you don't have file access rights. |
| 16536 | 16 | No | Cannot bulk load because the file "%ls" could not be opened. |
| 16537 | 16 | No | Openrowset statistics are not supported on %ls. |
| 16538 | 16 | No | You do not have required permission to execute '%ls'. |
| 16539 | 16 | No | Operation failed since the external data source '%ls' has underlying storage account that is not in the list of Outbound Firewall Rules on the server. Please add this storage account to the list of Outbound Firewall Rules on your server and retry the operation. |
| 16540 | 16 | No | Session context is not supported in distributed query execution. |
| 16541 | 16 | No | A %ls with the name "%ls" already exists. Use a different name for resource. |
| 16542 | 16 | No | %ls option is not supported. |
| 16543 | 16 | No | %ls is not supported for specified file format. |
| 16544 | 16 | No | The maximum reject threshold is reached. |
| 16545 | 10 | No | Warning: Rejected rows encountered during execution. |
| 16546 | 16 | No | Queries referencing variables are not supported in distributed processing mode. |
| 16547 | 16 | No | CosmosDb query does not support given bulk options. |
| 16548 | 16 | No | Credential with name '%.\*ls' has not been found or you do not have the permission to access it. |
| 16549 | 16 | No | Values in column %ls are formatted as JSON objects and cannot be written using CREATE EXTERNAL TABLE AS SELECT statement. Convert %ls column to a single VARCHAR or NVARCHAR column or a set of columns with explicitly defined types. |
| 16550 | 16 | No | EXECUTE %ls. Warning: Stored procedures cannot be permanently stored in master database. Script procedure and create it in other database. |
| 16551 | 16 | No | Bulk load data conversion error (truncation);%I64d;%d;%ls;%ls;%d;%ls. |
| 16552 | 16 | No | Data conversion error (type mismatch or invalid character for the specified codepage);%I64d;%d;%ls;%ls;%d;%ls. |
| 16553 | 16 | No | Bulk load data conversion error (overflow);%I64d;%d;%ls;%ls;%d;%ls. |
| 16554 | 16 | No | Operation failed due to an error in a background task. Please retry the operation. If the problem persists contact Microsoft Azure Customer Support. |
| 16555 | 17 | No | Operation failed due to an error while processing rejected rows. Intermediate results, if any, should be discarded as such results may not be complete. Please retry the operation. If the problem persists, contact Microsoft Azure Customer Support. |
| 16556 | 10 | No | Operation for removing intermediate results failed while processing rejected rows. Intermediate results, if any, should be manually deleted. |
| 16557 | 16 | No | Potential conversion error while reading VARCHAR column '%.\*ls' from UTF8 encoded text. Change database collation to a UTF8 collation or specify explicit column schema in WITH clause and assign UTF8 collation to VARCHAR columns. |
| 16558 | 10 | No | Potential conversion error while reading VARCHAR column '%.\*ls' from UTF8 encoded text. Change database collation to a UTF8 collation or specify explicit column schema in WITH clause and assign UTF8 collation to VARCHAR columns. |
| 16559 | 16 | No | CODEPAGE different than 65001 is not supported when CSV 2.0 is specified. |
| 16560 | 16 | No | Column '%s' of type '%s' is not compatible with external data type '%s', please try with '%s'. File/External table name: '%ls'. |
| 16561 | 16 | No | External table '%ls' is not accessible because content of directory cannot be listed. |
| 16562 | 16 | No | External table '%ls' is not accessible because location does not exist or it is used by another process. |
| 16563 | 16 | No | Format type '%.\*ls' already exists. |
| 16564 | 16 | No | Parser version '%.\*ls' for format type '%.\*ls' already exists. |
| 16565 | 16 | No | CREATE DATABASE failed. User database limit has been already reached (%d). |
| 16566 | 16 | No | A path in the Openrowset function cannot be empty. |
| 16567 | 16 | No | Format '%.\*ls' does not support extraction of file metadata only. |
| 16568 | 16 | No | Output path for rejected rows is too long. Max length of the path is nvarchar(260). |
| 16569 | 16 | No | Output path for rejected rows is too long. Max length of the path is nvarchar(1024). |
| 16570 | 10 | No | Use a collation that enables string predicate pushdown and file elimination on storage layer. |
| 16571 | 16 | No | Unable to retrieve user token details for external computation. |
| 16572 | 16 | No | Parser version '%.\*ls' for format type '%.\*ls' does not exist. |
| 16573 | 10 | No | Some info messages might been dropped. |
| 16574 | 10 | No | Query execution is canceled. Operation for removing intermediate results while processing rejected rows did not perform. Intermediate results, if any, should be manually deleted. |
| 16575 | 16 | No | Arithmetic overflow error converting a value to data type '%ls'. File/External table name '%ls', column '%ls'. Please try with '%ls'. |
| 16576 | 16 | No | Location provided by DATA_SOURCE '%.\*ls' cannot contain any wildcards. |
| 16577 | 16 | No | Number of wildcards in LOCATION must match the number of columns in PARTITION clause. |
| 16578 | 16 | No | The column name '%.\*ls' specified in the PARTITION option does not match any column specified in the columns list. |
| 16579 | 16 | No | A column has been specified more than once in the PARTITION list. Column '%.\*ls' is specified more than once. |
| 16580 | 16 | No | Openrowset is not supported. |
| 16581 | 16 | No | Cannot parse table options: %ls |
| 16582 | 16 | No | Internal error led to query cancellation: \[Diagnostics: '%.\*ls'\] |
| 16583 | 16 | No | The query must contain no more than %.\*ls OPENROWSET columns. |
| 16584 | 16 | No | Column '%ls' contains NULL values and cannot be used as PARTITION column. |
| 16585 | 16 | No | Column '%ls' contains path delimiter and cannot be used as PARTITION column. The actual value is '%ls'. |
| 16586 | 16 | No | Number of partition columns exceeds the maximum number of partition columns allowed which is %d. |
| 16587 | 16 | No | Number of created partitions exceeds the limit. There are more than %d files created. |
| 16588 | 16 | No | Virtual or partition columns found in Delta external table. |
| 16589 | 16 | No | Virtual or partition columns not supported for Delta external table. |
| 16590 | 16 | No | Invalid list of columns in PARTITION option. Only columns that expose wildcards are allowed and all such columns need to be listed. |
| [16591](../mssqlserver-16591-database-engine-error.md) | 16 | No | Multiple logical file paths limit has been reached. Statement contains %ld logical file paths, maximum allowed limit is %d. |
| 16592 | 10 | No | Warning: Unable to resolve path %ls. Error number %ld, Level %ld, State %ld, Message "%ls". |
| 16593 | 10 | No | Warning: Maximum number of warnings reached (%ld). Please try resolving warnings and resubmit the query. |
| [16594](../mssqlserver-16594-database-engine-error.md) | 16 | No | Path '%ls' was referenced multiple times in result set '%ls'. |
| 16595 | 16 | No | Database name '%ls' is reserved. Choose a different database name. |
| 16596 | 16 | No | The specified location is invalid: '%ls'. |
| 16597 | 16 | No | The specified storage account does not have hierarchical namespace enabled. |
| 16598 | 16 | No | Cannot access the specified location '%ls', because it does not exist or you do not have permission. |
| 16599 | 16 | No | An error occurred while attempting to delete the specified location '%ls' (HRESULT = '0x%x'). |
| 16601 | 16 | No | Credential of database '%ls' are invalid. |
| 16602 | 16 | No | Cannot delete sync agent '%ls' because it is used by sync member '%ls'. |
| 16603 | 16 | No | Cannot add database '%ls' into sync group because the database name is invalid. |
| 16604 | 16 | No | Hub database '%ls' is invalid. |
| 16605 | 16 | No | Member database '%ls' is invalid. |
| 16606 | 16 | No | Database '%ls' cannot be deleted because it is used as a sync metadata database which still contains sync groups and/or sync agents. |
| 16607 | 16 | No | Sync metadata database '%ls' is invalid. |
| 16608 | 16 | No | Cannot create or update sync group because the sync group name '%ls' is invalid. |
| 16609 | 16 | No | Cannot create or update sync group '%ls' because the conflict resolution policy is invalid. |
| 16610 | 16 | No | Cannot create sync group because the sync group name '%ls' is used. |
| 16611 | 16 | No | Cannot create or update sync group '%ls' because the sync schema contains circular reference. |
| 16612 | 16 | No | Cannot create or update sync group '%ls' because the table '%ls' in sync schema contains no clustered index. |
| 16613 | 16 | No | Cannot delete sync group '%ls' because the sync group is syncing. |
| 16614 | 16 | No | Cannot create or update sync group '%ls' because database '%ls' is invalid. |
| 16615 | 16 | No | Cannot create or update sync group '%ls' because the sync interval is invalid. |
| 16616 | 16 | No | Cannot update sync schema because the data type change is not supported. |
| 16617 | 16 | No | Sync group '%ls' is not ready to update sync schema because there are some ongoing operations on the sync group. |
| 16618 | 16 | No | Cannot update sync schema because some columns are missing in database '%ls'. |
| 16619 | 16 | No | Cannot update sync schema because some tables are missing in database '%ls'. |
| 16620 | 16 | No | Cannot update sync schema because the format of sync schema is invalid. |
| 16621 | 16 | No | Sync group '%ls' is not in active state. Make sure the sync schema of it is set. |
| 16622 | 16 | No | Hub database '%ls' is suspended because the credential of it is invalid. |
| 16623 | 16 | No | Sync group '%ls' is invalid. |
| 16624 | 16 | No | Cannot create or update sync member because the sync member name '%ls' is invalid. |
| 16625 | 16 | No | Cannot create or update the sync member '%ls' because the database type '%ls' provided is invalid. |
| 16626 | 16 | No | Cannot create or update the sync member '%ls' because the sync direction '%ls' provided is invalid. |
| 16627 | 16 | No | Cannot create or update the sync member '%ls' because the sync agent '%ls' provided is invalid. |
| 16628 | 16 | No | Cannot create or update the sync member '%ls' because the SQL Server database ID '%ls' provided is invalid. |
| 16629 | 16 | No | Cannot create sync member because the sync member name '%ls' provided is used. |
| 16630 | 16 | No | Cannot create sync member '%ls' because the database '%ls' provided is already added as a sync member. |
| 16631 | 16 | No | Cannot delete sync member '%ls' when it is syncing. |
| 16632 | 16 | No | Sync member '%ls' does not exist. |
| 16633 | 16 | No | Cannot create sync agent because the sync agent name '%ls' provided is used. |
| 16634 | 16 | No | Sync agent '%ls' is invalid. |
| 16635 | 16 | No | Cannot create sync group '%ls' because the maximum number of basic sync groups can be created is %d. |
| 16636 | 16 | No | Cannot create sync member '%ls' because the maximum number of sync members can be created in a sync group is %d. |
| 16637 | 16 | No | Cannot create or update sync group '%ls' because the maximum count of tables in sync schema is %d. |
| 16638 | 16 | No | Cannot create or update sync group '%ls' because the table '%ls' in sync schema contains no primary key. |
| 16639 | 16 | No | Cannot create or update sync group '%ls' because the sync schema provided contains unsupported column data type. |
| 16640 | 16 | No | Cannot refresh schema of the database '%ls'. |
| 16641 | 16 | No | Cannot create sync agent '%ls' under a different SQL Server than the one of sync metadata database. |
| 16642 | 16 | No | Conflict logging retention period parameter is required if conflict logging is turned on. |
| 16643 | 16 | No | Data Sync conflict logging feature is not enabled. |
| 16644 | 16 | No | Value for data Sync conflict logging retention in days should be positive or zero. |
| 16645 | 16 | No | The sync group is already being dropped. |
| 16646 | 16 | No | The sync member is already being dropped. |
| 16647 | 16 | No | Failed to perform data sync operation: %ls |
| 16648 | 16 | No | The sync database specified (%ls\\%ls) does not match the existing sync database (%ls\\%ls). |
| 16649 | 16 | No | Hub logical server %ls does not exist. |
| 16650 | 16 | No | The sync agent %ls already exists. |
| 16651 | 16 | No | The sync agent with the id %ls already exists. |
| 16652 | 16 | No | Cannot update the sync group because it is currently being dropped. |
| 16653 | 16 | No | Cannot use datawarehouse edition in data sync. |
| 16654 | 16 | No | Cannot use logical master in data sync. |
| 16701 | 16 | No | A conflict operation on this LTR backup is still in progress. |
| 16702 | 16 | No | LTR backup migration %ls feature is not supported on subscription '%ls'. |
| 16703 | 16 | No | Copy LTR backup from source subscription '{0}' to target subscription '{1}' is not allowed. |
| 16704 | 16 | No | A required parameter was not provided for LTR backup %ls operation. Missing parameter '%ls' |
| 16705 | 16 | No | LTR Copy feature is not supported to copy LTR backups within same server. |
| 16706 | 16 | No | LTR backup specified for LTR backup %ls operation does not exists. |
| 16707 | 16 | No | Target server '%ls' not found or is not ready for LTR backup copy operation. |
| 16708 | 16 | No | Target Database '%ls' not found on server '%ls' for LTR backup copy operation. |
| 16709 | 16 | No | Failed to start LTR backup copy request in target region. |
| 16710 | 16 | No | Specified Backup Storage Redundancy '%ls' is not supported in target region. |
| 16711 | 16 | No | Active backup redundancy '%ls' of database '%ls' does not match the requested backup redundancy of LTR backup '%ls'. |
| 16712 | 16 | No | LTR Migration requests are not supported for databases of type '%ls'. |
| 16713 | 16 | No | Another LTR backup with same backup time for target database. |
| 16714 | 16 | No | Copy operation failed for LTR backup blobs. |
| 16715 | 16 | No | Restore verification failed after max attempts were reached. Last failure reason: %ls |
| 16716 | 16 | No | Restore verification failed. Failure reason: %ls |
| 16717 | 16 | No | LTR backup specified for LTR backup %ls operation does not exists. |
| 16718 | 16 | No | Another LTR backup exist with same backup time for target database. |
| 16719 | 16 | No | Changing backup storage redundancy is not allowed for LTR Copy operations. |
| 16720 | 16 | No | LTR Backup Copy/Storage Update feature is not supported for Hyperscale Database LTR Backups currently. |
| 16721 | 16 | No | LTR Migration not supported between source and target database with different is_ledger_on property. |
| 16722 | 16 | No | Cannot change service objective for %ls to %ls as long-term retention is not supported yet on Hyperscale. Please disable long-term retention on the database and retry |
| 16901 | 16 | No | %hs: This feature has not been implemented yet. |
| 16902 | 16 | No | %ls: The value of the parameter %ls is invalid. |
| 16903 | 16 | No | The "%ls" procedure was called with an incorrect number of parameters. |
| 16904 | 16 | No | sp_cursor: optype: You can only specify ABSOLUTE in conjunction with DELETE or UPDATE. |
| 16905 | 16 | No | The cursor is already open. |
| 16906 | 17 | No | Temporary storage used by the cursor to store large object variable values referred by the cursor query is not usable any more. |
| 16907 | 16 | No | %hs is not allowed in cursor statements. |
| 16909 | 16 | No | %ls: The cursor identifier value provided (%x) is not valid. |
| 16910 | 16 | No | The cursor %.\*ls is currently used by another statement. |
| 16911 | 16 | No | %hs: The fetch type %hs cannot be used with forward only cursors. |
| 16914 | 16 | No | The "%ls" procedure was called with too many parameters. |
| 16915 | 16 | No | A cursor with the name '%.\*ls' already exists. |
| 16916 | 16 | No | A cursor with the name '%.\*ls' does not exist. |
| 16917 | 16 | No | Cursor is not open. |
| 16922 | 16 | No | Cursor Fetch: Implicit conversion from data type %s to %s is not allowed. |
| 16924 | 16 | No | Cursorfetch: The number of variables declared in the INTO list must match that of selected columns. |
| 16925 | 16 | No | The fetch type %hs cannot be used with dynamic cursors. |
| 16926 | 16 | No | sp_cursoroption: The column ID (%d) does not correspond to a text, ntext, or image column. |
| 16927 | 16 | No | Cannot fetch into text, ntext, and image variables. |
| 16928 | 16 | No | sp_cursor: Exec statement is not allowed as source for cursor insert. |
| 16929 | 16 | No | The cursor is READ ONLY. |
| 16930 | 16 | No | The requested row is not in the fetch buffer. |
| 16931 | 16 | No | There are no rows in the current fetch buffer. |
| 16932 | 16 | No | The cursor has a FOR UPDATE list and the requested column to be updated is not in this list. |
| 16933 | 16 | No | The cursor does not include the table being modified or the table is not updatable through the cursor. |
| 16934 | 10 | No | Optimistic concurrency check failed. The row was modified outside of this cursor. |
| 16935 | 16 | No | No parameter values were specified for the sp_cursor-%hs statement. |
| 16936 | 16 | No | sp_cursor: One or more values parameters were invalid. |
| 16937 | 16 | No | A server cursor cannot be opened on the given statement or statements. Use a default result set or client cursor. |
| 16938 | 16 | No | sp_cursoropen/sp_cursorprepare: The statement parameter can only be a batch or a stored procedure with a single select, without FOR BROWSE, COMPUTE BY, or variable assignments. |
| 16941 | 16 | No | Cursor updates are not allowed on tables opened with the NOLOCK option. |
| 16942 | 16 | No | Could not generate asynchronous keyset. The cursor has been deallocated. |
| 16943 | 16 | No | Could not complete cursor operation because the table schema changed after the cursor was declared. |
| 16945 | 16 | No | The cursor was not declared. |
| 16946 | 16 | No | Could not open the cursor because one or more of its tables have gone out of scope. |
| 16947 | 16 | No | No rows were updated or deleted. |
| 16948 | 16 | No | The variable '%.\*ls' is not a cursor variable, but it is used in a place where a cursor variable is expected. |
| 16949 | 16 | No | The variable '%.\*ls' is a cursor variable, but it is used in a place where a cursor variable is not valid. |
| 16950 | 10 | No | The variable '%.\*ls' does not currently have a cursor allocated to it. |
| 16951 | 16 | No | The variable '%.\*ls' cannot be used as a parameter because a CURSOR OUTPUT parameter must not have a cursor allocated to it before execution of the procedure. |
| 16952 | 16 | No | A cursor variable cannot be used as a parameter to a remote procedure call. |
| 16953 | 10 | No | Remote tables are not updatable. Updatable keyset-driven cursors on remote tables require a transaction with the REPEATABLE_READ or SERIALIZABLE isolation level spanning the cursor. |
| 16954 | 16 | No | Executing SQL directly; no cursor. |
| 16955 | 16 | No | Could not create an acceptable cursor. |
| 16956 | 10 | No | The created cursor is not of the requested type. |
| 16957 | 16 | No | FOR UPDATE cannot be specified on a READ ONLY cursor. |
| 16958 | 16 | No | Could not complete cursor operation because the set options have changed since the cursor was declared. |
| 16959 | 16 | No | Unique table computation failed. |
| 16960 | 16 | No | You have reached the maximum number of cursors allowed. |
| 16961 | 10 | No | One or more FOR UPDATE columns have been adjusted to the first instance of their table in the query. |
| 16962 | 16 | No | The target object type is not updatable through a cursor. |
| 16963 | 16 | No | You cannot specify scroll locking on a cursor that contains a remote table. |
| 16964 | 16 | No | For the optimistic cursor, timestamp columns are required if the update or delete targets are remote. |
| 16965 | 16 | No | Cursor scroll locks were invalidated due to a transaction defect. Reissue the UPDATE or DELETE statement after a cursor fetch. |
| 16966 | 16 | No | %ls: Specified concurrency control option %d (%ls) is incompatible with static or fast forward only cursors. Only read-only is compatible with static or fast forward only cursors. |
| 16992 | 16 | No | The cursor operation is required to wait for cursor asynchronous population to complete. However, at this point the transaction cannot be yielded to let the asynchronous population to continue. |
| 16996 | 16 | No | %ls cannot take output parameters. |
| 16998 | 16 | No | The asynchronous cursor worktable population thread spawn failed. |
| 16999 | 20 | Yes | Internal Cursor Error: The cursor is in an invalid state. |
| 17000 | 10 | No | Usage: sp_autostats \<table_name\> \[, {ON\|OFF} \[, \<index_name\>\] \] |
| 17001 | 16 | Yes | Failure to send an event notification instance of type '%s' on conversation handle '%s'. Error Code = '%s'. |
| 17002 | 16 | Yes | Failed to post QUEUE_ACTIVATION event. Error code: '0x%s'. |
| 17003 | 16 | Yes | Closed event notification conversation endpoint with handle '%s', due to the following error: '%.\*ls'. |
| 17004 | 16 | Yes | Event notification conversation on dialog handle '%s' closed without an error. |
| 17005 | 16 | Yes | Event notification '%ls' in database '%ls' dropped due to send time service broker errors. Check to ensure the conversation handle, service broker contract, and service specified in the event notification are active. |
| 17049 | 16 | Yes | Unable to cycle error log file from '%ls' to '%ls' due to OS error '%s'. A process outside of SQL Server may be preventing SQL Server from reading the files. As a result, errorlog entries may be lost and it may not be possible to view some SQL Server errorlogs. Make sure no other processes have locked the file with write-only access." |
| 17051 | 16 | Yes | SQL Server evaluation period has expired. |
| [17053](../mssqlserver-17053-database-engine-error.md) | 16 | Yes | %ls: Operating system error %ls encountered. |
| 17054 | 16 | Yes | The current event was not reported to the operating system error log. Operating system error = %s. You may need to clear the operating system error log if it is full. |
| 17056 | 10 | Yes | The evaluation period for your edition of SQL Server expires in %d day(s). |
| 17057 | 16 | Yes | Security context for operating system objects could not be created. SQL Server cannot be started. Look for corresponding entries in the event viewer to help diagnose the root cause. |
| 17058 | 16 | Yes | initerrlog: Could not open error log file '%s'. Operating system error = %s. |
| 17060 | 10 | Yes | %s |
| 17061 | 10 | Yes | Error: %d Severity: %d State: %d %s |
| 17063 | 16 | Yes | Error: %d Severity: %d State: %d %s |
| [17065](../mssqlserver-17065-database-engine-error.md) | 16 | Yes | SQL Server Assertion: File: \<%s\>, line = %d Failed Assertion = '%s' %s. This error may be timing-related. If the error persists after rerunning the statement, use DBCC CHECKDB to check the database for structural integrity, or restart the server to ensure in-memory data structures are not corrupted. |
| [17066](../mssqlserver-17066-database-engine-error.md) | 16 | Yes | SQL Server Assertion: File: \<%s\>, line=%d Failed Assertion = '%s'. This error may be timing-related. If the error persists after rerunning the statement, use DBCC CHECKDB to check the database for structural integrity, or restart the server to ensure in-memory data structures are not corrupted. |
| [17067](../mssqlserver-17067-database-engine-error.md) | 16 | Yes | SQL Server Assertion: File: \<%s\>, line = %d %s. This error may be timing-related. If the error persists after rerunning the statement, use DBCC CHECKDB to check the database for structural integrity, or restart the server to ensure in-memory data structures are not corrupted. |
| 17068 | 10 | No | PrintStack Request |
| 17069 | 10 | Yes | %s |
| 17070 | 16 | Yes | Clustered instances are not supported on this edition of SQL Server. |
| 17071 | 16 | Yes | SQL Server could not start due to a boot failure. Operating system error = %s. |
| 17072 | 17 | Yes | The Extended Event session could not be created. |
| 17073 | 16 | Yes | Executing 'sp_server_diagnostics' stored procedure in repeat mode with 'insert into' clause is not allowed. |
| 17074 | 16 | Yes | Assertion "%ls" with message "%ls" at \<%ls\>:%ld failed. |
| 17075 | 16 | Yes | Assertion "%ls" at \<%ls\>:%ld failed. |
| 17076 | 21 | Yes | Error spawning System Health Monitor thread: %ls |
| 17101 | 10 | Yes | (c) Microsoft Corporation. |
| 17102 | 16 | Yes | Failed to initialize Distributed COM (CoInitializeEx returned %lx). Heterogeneous queries and remote procedure calls are disabled. Check the DCOM configuration using Component Services in Control Panel. |
| 17103 | 10 | Yes | All rights reserved. |
| 17104 | 10 | Yes | Server process ID is %ld. |
| 17105 | 10 | Yes | Could not open master database in system task thread context. Terminating server. |
| 17106 | 10 | Yes | Common Criteria compliance mode is enabled. This is an informational message only; no user action is required. |
| 17107 | 10 | No | Perfmon counters for resource governor pools and groups failed to initialize and are disabled. |
| 17108 | 10 | Yes | Password policy update was successful. |
| 17109 | 10 | Yes | FallBack certificate was successfully created. |
| 17110 | 10 | Yes | Registry startup parameters: %.\*ls |
| 17111 | 10 | Yes | Logging SQL Server messages in file '%s'. |
| [17112](../mssqlserver-17112-database-engine-error.md) | 16 | Yes | An invalid startup option '%s' was supplied, either from the registry or the command prompt. Correct or remove the option. |
| 17113 | 16 | Yes | Error %ls occurred while opening file '%ls' to obtain configuration information at startup. An invalid startup option might have caused the error. Verify your startup options, and correct or remove them if necessary. |
| 17114 | 16 | Yes | Error %ls occurred while opening file '%ls' to obtain configuration information at startup time. An invalid startup option might have caused the error. Verify your startup options, and correct or remove them if necessary. |
| 17115 | 10 | Yes | Command Line Startup Parameters:%.\*ls |
| 17116 | 16 | Yes | Failed to initialize distributed COM; DCOM is not installed. Heterogeneous queries and remote procedure calls are disabled. Check the DCOM configuration using Component Services in Control Panel. |
| 17117 | 10 | Yes | The tempdb database has %ld data file(s). |
| 17118 | 10 | Yes | Database Instant File Initialization: %S_MSG. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required. |
| 17119 | 10 | Yes | The number of concurrent user connections was reduced to %ld, because it exceeded the allowable limit for this edition of SQL Server. To avoid this message in the future, use sp_configure to permanently adjust the number of user connections within the licensed limit. |
| [17120](../mssqlserver-17120-database-engine-error.md) | 16 | Yes | SQL Server could not spawn %s thread. Check the SQL Server error log and the operating system error log for information about possible related problems. |
| 17121 | 10 | Yes | SQL Server is started with trace flag %d, this may cause user to see some error messages masked using '%ls'. |
| 17122 | 10 | Yes | Trace flag %d is discontinued. Use the options provided with ALTER DATABASE. |
| 17123 | 10 | Yes | Logging to event log is disabled. Startup option '-%c' is supplied, either from the registry or the command prompt. |
| 17124 | 10 | Yes | SQL Server has been configured for lightweight pooling. This is an informational message; no user action is required. |
| 17125 | 10 | Yes | Using dynamic lock allocation. Initial allocation of %I64u Lock blocks and %I64u Lock Owner blocks per node. This is an informational message only. No user action is required. |
| 17126 | 10 | Yes | SQL Server is now ready for client connections. This is an informational message; no user action is required. |
| 17127 | 16 | Yes | initdata: No memory for kernel buffer hash table. |
| [17128](../mssqlserver-17128-database-engine-error.md) | 16 | Yes | initdata: No memory for kernel buffers. |
| 17129 | 10 | Yes | initconfig: Warning: affinity specified is not valid. Defaulting to no affinity. Use ALTER SERVER CONFIGURATION SET PROCESS AFFINITY to configure the system to be compatible with the CPU mask on the system. You can also configure the system based on the number of licensed CPUs. |
| [17130](../mssqlserver-17130-database-engine-error.md) | 16 | Yes | Not enough memory for the configured number of locks. Attempting to start with a smaller lock hash table, which may impact performance. Contact the database administrator to configure more memory for this instance of the Database Engine. |
| 17131 | 16 | Yes | Server startup failed due to insufficient memory for descriptor hash tables. Reduce non-essential memory load or increase system memory. |
| [17132](../mssqlserver-17132-database-engine-error.md) | 16 | Yes | Server startup failed due to insufficient memory for descriptor. Reduce non-essential memory load or increase system memory. |
| 17133 | 16 | Yes | Launch of startup procedure '%s' failed. |
| 17134 | 10 | Yes | The tempdb database data files are not configured with the same initial size and autogrowth settings. To reduce potential allocation contention, the initial size and autogrowth of the files should be same. |
| 17135 | 10 | Yes | Launched startup procedure '%s'. |
| 17136 | 10 | Yes | Clearing tempdb database. |
| 17137 | 10 | Yes | Starting up database '%.\*ls'. |
| 17138 | 16 | Yes | Unable to allocate enough memory to start '%ls'. Reduce non-essential memory load or increase system memory. |
| 17139 | 10 | Yes | The SQL Server image %ls was allocated using the large pages option. |
| 17140 | 16 | Yes | Could not dispatch SQL Server by Service Control Manager. Operating system error = %s. |
| 17141 | 16 | Yes | Could not register Service Control Handler. Operating system error = %s. |
| [17142](../mssqlserver-17142-database-engine-error.md) | 16 | Yes | SQL Server service has been paused. No new connections will be allowed. To resume the service, use SQL Computer Manager or the Services application in Control Panel. |
| 17143 | 16 | Yes | %s: Could not set Service Control Status. Operating system error = %s. |
| 17144 | 10 | Yes | SQL Server is not allowing new connections because the Service Control Manager requested a pause. To resume the service, use SQL Computer Manager or the Services application in Control Panel. |
| 17145 | 10 | Yes | Service Control Handler received an invalid control code = %d. |
| 17146 | 10 | Yes | SQL Server is allowing new connections in response to 'continue' request from Service Control Manager. This is an informational message only. No user action is required. |
| [17147](../mssqlserver-17147-database-engine-error.md) | 10 | Yes | SQL Server is terminating because of a system shutdown. This is an informational message only. No user action is required. |
| [17148](../mssqlserver-17148-database-engine-error.md) | 10 | Yes | SQL Server is terminating in response to a 'stop' request from Service Control Manager. This is an informational message only. No user action is required. |
| 17149 | 10 | Yes | Using the static lock allocation specified in the locks configuration option. Allocated %I64u Lock blocks and %I64u Lock Owner blocks per node. This is an informational message only. No user action is required. |
| 17150 | 10 | Yes | Lock partitioning is enabled. This is an informational message only. No user action is required. |
| 17152 | 10 | Yes | Node configuration: node %ld: CPU mask: 0x%0\*I64x:%u Active CPU mask: 0x%0\*I64x:%u. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required. |
| 17153 | 10 | Yes | Processor affinity turned on: node %d, processor mask 0x%0\*I64x. Threads will execute on CPUs per affinity settings. This is an informational message; no user action is required. |
| 17155 | 10 | Yes | I/O affinity turned on, processor mask 0x%0\*I64x. Disk I/Os will execute on CPUs per affinity I/O mask/affinity64 mask config option. This is an informational message only; no user action is required. |
| 17156 | 16 | Yes | initeventlog: Could not initiate the EventLog Service for the key '%s', last error code is %d. |
| 17158 | 10 | Yes | The server resumed execution after being idle %d seconds. This is an informational message only. No user action is required. |
| 17159 | 10 | Yes | The server is idle. This is an informational message only. No user action is required. |
| 17161 | 10 | Yes | SQL Server could not use the NO_BUFFERING option during I/O, because the master file sector size, %d, is incorrect. Move the master file to a drive with a correct sector size. |
| 17162 | 10 | Yes | SQL Server is starting at normal priority base (=7). This is an informational message only. No user action is required. |
| 17163 | 10 | Yes | SQL Server is starting at high priority base (=13). This is an informational message only. No user action is required. |
| 17164 | 10 | Yes | SQL Server detected %d sockets with %d cores per socket and %d logical processors per socket, %d total logical processors; using %d logical processors based on SQL Server licensing. This is an informational message; no user action is required. |
| 17165 | 10 | Yes | The RANU instance is terminating in response to its internal time out. This is an informational message only. No user action is required. |
| 17166 | 10 | Yes | Initializing Microsoft Distributed Transaction Coordinator (MS DTC) resource manager \[%ls\] for server instance %ls. This is an informational message only. No user action is required. |
| 17167 | 10 | Yes | Support for distributed transactions was not enabled for this instance of the Database Engine because it was started using the minimal configuration option. This is an informational message only. No user action is required. |
| 17169 | 10 | Yes | Unable to locate kernel HTTP driver Httpapi.dll in path. SQL Server native HTTP support is not available. Error: 0x%lx Your operating system may not support the kernel HTTP driver. |
| 17170 | 10 | Yes | SQL Server native HTTP support is not available. Could not find function entry point '%hs' in %hs. Error 0x%lx. Native HTTP access to SQL Server requires a later version of the operating system. |
| 17171 | 10 | Yes | SQL Server native HTTP support failed and will not be available. '%hs()' failed. Error 0x%lx. |
| 17172 | 16 | Yes | SNIInitialize() failed with error 0x%lx. |
| 17173 | 10 | Yes | Ignoring trace flag %u specified during startup. It is either an invalid trace flag or a trace flag that cannot be specified during server startup. |
| 17174 | 10 | Yes | Unable to initialize SQL Server native HTTP support due to insufficient resources. HTTP access to SQL Server will not be available. Error 0x%lx. This error typically indicates insufficient memory. Reduce non-essential memory load or increase system memory. |
| 17175 | 10 | Yes | The registry settings for SNI protocol configuration are incorrect. The server cannot accept connection requests. Error: 0x%lx. Status: 0x%lx. |
| 17176 | 10 | Yes | This instance of SQL Server last reported using a process ID of %s at %s (local) %s (UTC). This is an informational message only; no user action is required. |
| 17177 | 10 | Yes | This instance of SQL Server has been using a process ID of %s since %s (local) %s (UTC). This is an informational message only; no user action is required. |
| 17178 | 10 | Yes | Warning: Enterprise Server/CAL license used for this instance. This edition limits SQL Engine CPU utilization to 20 physical cores, or 40 logical cores with Hyper-threading enabled. |
| 17179 | 10 | Yes | SQL Server detected %d sockets with %d cores per socket and %d logical processors per socket, %d total logical processors; using %d logical processors based on SQL Server licensing. |
| 17181 | 16 | Yes | SNIInitializeListener() failed with error 0x%lx. |
| [17182](../mssqlserver-17182-database-engine-error.md) | 16 | Yes | TDSSNIClient initialization failed with error 0x%lx, status code 0x%lx. Reason: %S_MSG %.\*ls |
| 17183 | 10 | Yes | Attempting to cycle error log. This is an informational message only; no user action is required. |
| 17184 | 10 | Yes | The error log has been reinitialized. See the previous log for older entries. |
| 17185 | 16 | Yes | Unable to update password policy. |
| 17186 | 16 | Yes | Failed to enqueue %s task. There may be insufficient memory. |
| 17187 | 16 | Yes | SQL Server is not ready to accept new client connections. Wait a few minutes before trying again. If you have access to the error log, look for the informational message that indicates that SQL Server is ready before trying to connect again. %.\*ls |
| 17188 | 16 | Yes | SQL Server cannot accept new connections, because it is shutting down. The connection has been closed.%.\*ls |
| 17189 | 16 | Yes | SQL Server failed with error code 0x%x to spawn a thread to process a new login or connection. Check the SQL Server error log and the operating system error log for information about possible related problems.%.\*ls |
| 17190 | 16 | Yes | Initializing the FallBack certificate failed with error code: %d, state: %d, error number: %d. |
| 17191 | 16 | Yes | Cannot accept a new connection because the session has been terminated. This error occurs when a new batch execution is attempted on a session that is logging out, or when a severe error is encountered upon connection. Check the error log to see if this session was terminated by a KILL command or because of severe errors.%.\*ls |
| 17192 | 10 | Yes | Dedicated admin connection support was not started because of error 0x%lx, status code: 0x%lx. This error typically indicates a socket-based error, such as a port already in use. |
| 17193 | 10 | Yes | SQL Server native SOAP support is ready for client connections. This is an informational message only. No user action is required. |
| [17194](../mssqlserver-17194-database-engine-error.md) | 16 | Yes | The server was unable to load the SSL provider library needed to log in; the connection has been closed. SSL is used to encrypt either the login sequence or all communications, depending on how the administrator has configured the server. See Books Online for information on this error message: %d %.\*ls %.\*ls |
| 17195 | 16 | Yes | The server was unable to complete its initialization sequence because the available network libraries do not support the required level of encryption. The server process has stopped. Before restarting the server, verify that SSL certificates have been installed. See Books Online topic "Configuring Client Protocols and Network Libraries". |
| 17196 | 10 | Yes | Preparing for eventual growth to %d GB with Hot Add Memory. |
| 17197 | 16 | Yes | Login failed due to timeout; the connection has been closed. This error may indicate heavy server load. Reduce the load on the server and retry login.%.\*ls |
| 17198 | 16 | Yes | Connection failed because the endpoint could not be found. This may result if an endpoint is dropped while a connection attempt is in progress. Attempt to connect to a different endpoint on the server.%.\*ls |
| 17199 | 10 | Yes | Dedicated administrator connection support was not started because it is disabled on this edition of SQL Server. If you want to use a dedicated administrator connection, restart SQL Server using the trace flag %d. This is an informational message only. No user action is required. |
| 17200 | 16 | Yes | Changing the remote access settings for the Dedicated Admin Connection failed with error 0x%lx, status code 0x%lx. |
| 17201 | 10 | Yes | Dedicated admin connection support was established for listening locally on port %d. |
| 17202 | 10 | Yes | Dedicated admin connection support was established for listening remotely on port %d. |
| 17203 | 16 | Yes | SQL Server cannot start on this machine. The processor(s) (CPU) model does not support all instructions needed for SQL Server to run. Refer to the System Requirements section in BOL for further information. |
| [17204](../mssqlserver-17204-database-engine-error.md) | 16 | Yes | %ls: Could not open file %ls for file number %d. OS error: %ls. |
| 17205 | 10 | Yes | File %ls in database %ls has been set to sparse by the file system but does not belong to a database snapshot. The file should be restored to correct the problem. |
| 17206 | 10 | Yes | File %ls, file number %d for dbid %d is successfully %ls mapped for use by Hybrid Buffer Pool. |
| [17207](../mssqlserver-17207-database-engine-error.md) | 16 | Yes | %ls: Operating system error %ls occurred while creating or opening file '%ls'. Diagnose and correct the operating system error, and retry the operation. |
| 17208 | 16 | Yes | %s: File '%s' has an incorrect size. It is listed as %d MB, but should be %d MB. Diagnose and correct disk failures, and restore the database from backup. |
| 17209 | 10 | Yes | File %ls, file number %d for dbid %d: File size is not configured multiple of the minimum size of a large page for Hybrid Buffer Pool. |
| 17253 | 10 | Yes | SQL Server cannot use the NO_BUFFERING option during I/O on this file, because the sector size for file '%s', %d, is invalid. Move the file to a disk with a valid sector size. |
| 17255 | 10 | Yes | Secondary TempDB file '%.\*ls' resides on a removable drive and therefore will not be attached during startup. |
| 17256 | 10 | Yes | Secondary TempDB file '%.\*ls' will not be attached during TempDB startup; Drive check failed with error '%ld'. |
| 17257 | 10 | Yes | System error while trying to initialize disk info; Error '%ld' |
| 17258 | 10 | Yes | No free space in the TempDB database |
| 17259 | 10 | Yes | Dedicated admin connection support was established for listening locally on named pipe \[ %s \]. |
| 17260 | 10 | Yes | Dedicated admin connection support was established for listening remotely on named pipe \[ %s \]. |
| 17261 | 16 | Yes | initdata: No shared memory for kernel buffers. |
| 17262 | 16 | Yes | Replicated master not available for server state initialization during startup. |
| 17263 | 16 | Yes | Contained availability group master database not available for server state initialization during startup. |
| 17264 | 10 | Yes | CPU vectorization level(s) detected: %ls |
| [17300](../mssqlserver-17300-database-engine-error.md) | 16 | Yes | SQL Server was unable to run a new system task, either because there is insufficient memory or the number of configured sessions exceeds the maximum allowed in the server. Verify that the server has adequate memory. Use sp_configure with option 'user connections' to check the maximum number of user connections allowed. Use sys.dm_exec_sessions to check the current number of sessions, including user processes. |
| 17303 | 16 | Yes | The session with SPID %d was found to be invalid during termination, possibly because of corruption in the session structure. Contact Product Support Services. |
| 17305 | 16 | Yes | SQL server is started in a safe boot mode. No new connections can be created. This is informational message. |
| 17306 | 16 | Yes | Failed to exit safe mode either becuase we are not in safe mode or due to an error. |
| 17307 | 16 | Yes | Failed to boot database in safe mode. |
| 17308 | 16 | Yes | %s: Process %d generated an access violation. SQL Server is terminating this process. |
| 17310 | 20 | Yes | A user request from the session with SPID %d generated a fatal exception. SQL Server is terminating this session. Contact Product Support Services with the dump produced in the log directory. |
| 17311 | 16 | Yes | SQL Server is terminating because of fatal exception %lx. This error may be caused by an unhandled Win32 or C++ exception, or by an access violation encountered during exception handling. Check the SQL error log for any related stack dumps or messages. This exception forces SQL Server to shutdown. To recover from this error, restart the server (unless SQLAgent is configured to auto restart). |
| 17312 | 16 | Yes | SQL Server is terminating a system or background task %s due to errors in starting up the task (setup state %d). |
| 17313 | 10 | Yes | Unable to locate driver ntdll.dll in path. SQL Server native HTTP support is not available. Error: 0x%lx Your operating system may not support this driver. |
| 17401 | 10 | Yes | Server resumed execution after being idle %d seconds: user activity awakened the server. This is an informational message only. No user action is required. |
| 17403 | 10 | Yes | Server resumed execution after being idle %d seconds. Reason: timer event. |
| 17404 | 10 | Yes | The server resumed execution after being idle for %d seconds. |
| 17405 | 24 | Yes | An image corruption/hotpatch detected while reporting exceptional situation. This may be a sign of a hardware problem. Check SQLDUMPER_ERRORLOG.log for details. |
| 17406 | 10 | Yes | Server resumed execution after being idle %d seconds. Reason: resource pressure. |
| 17407 | 10 | Yes | The automatic soft-NUMA is already set to '%S_MSG'. No further action is necessary. |
| 17408 | 10 | Yes | The automatic soft-NUMA configuration has been set to '%S_MSG'. Restart SQL server for the new setting to take effect. |
| 17409 | 10 | Yes | Automatic soft-NUMA was enabled because SQL Server has detected hardware NUMA nodes with greater than %lu physical cores. |
| 17410 | 10 | Yes | Automatic soft-NUMA was not enabled, because 'NodeConfiguration' key was detected in the registry at path '%ls'. Disable registry based soft-NUMA configuration in order to activate the automatic soft-NUMA configuration. |
| 17411 | 10 | Yes | Hardware offload configuration hasn't changed. Current configuration (0x%x) and mode (0x%x). No action required. |
| 17412 | 10 | Yes | Hardware offload configuration has changed. Current configuration (0x%x) and mode (0x%x). New configuration (0x%x) and mode (0x%x). Restart SQL Server for the new configuration to take effect. |
| 17413 | 10 | Yes | Loading accelerator library %.\*ls failed with error 0x%x. |
| 17414 | 10 | Yes | Retrieving the address of an exported function %.\*ls in accelerator library %.\*ls failed with error 0x%x. |
| 17415 | 10 | Yes | %.\*ls component enumeration failed with zero component count. |
| 17416 | 10 | Yes | %.\*ls component enumeration failed with mismatch in component count. |
| 17417 | 10 | Yes | %.\*ls %.\*ls not compatible with SQL Server. |
| 17418 | 10 | Yes | Detected %.\*ls %.\*ls. |
| 17419 | 10 | Yes | %.\*ls hardware detected on the system. |
| 17420 | 10 | Yes | %.\*ls hardware not found on the system. |
| 17431 | 10 | Yes | %.\*ls initialization failed with error %d. |
| 17432 | 10 | Yes | %.\*ls initialization succeeded. |
| 17433 | 10 | Yes | %.\*ls session creation failed with error %d. |
| 17434 | 10 | Yes | %.\*ls session successfully created. |
| 17435 | 10 | Yes | %.\*ls will be used in hardware mode. |
| 17436 | 10 | Yes | This edition of SQL Server supports only software mode. %.\*ls will be used in software mode. |
| 17437 | 10 | Yes | %.\*ls will be used in software mode. |
| 17438 | 10 | Yes | %.\*ls session alive check failed with error %d. |
| 17439 | 10 | Yes | %.\*ls session tear down failed with error %d. |
| 17440 | 10 | Yes | %.\*ls session close failed with error %d. |
| 17441 | 10 | Yes | This operation requires %.\*ls libraries to be loaded. |
| 17442 | 10 | Yes | SQL Server detected the following NUMA node configuration (NUMA Node number %d, Processor Group number %d, CPU Mask 0x%0\*I64x). |
| 17550 | 10 | Yes | DBCC TRACEON %d, server process ID (SPID) %d. This is an informational message only; no user action is required. |
| 17551 | 10 | Yes | DBCC TRACEOFF %d, server process ID (SPID) %d. This is an informational message only; no user action is required. |
| 17557 | 16 | Yes | DBCC DBRECOVER failed for database ID %d. Restore the database from a backup. |
| 17558 | 10 | Yes | Bypassing recovery for database ID %d. This is an informational message only. No user action is required. |
| 17560 | 10 | Yes | DBCC DBREPAIR: '%ls' index restored for '%ls.%ls'. |
| 17561 | 10 | Yes | %ls index restored for %ls.%ls. |
| 17572 | 16 | Yes | DBCC cannot free DLL '%ls'. SQL Server requires this DLL in order to function properly. |
| 17573 | 10 | Yes | CHECKDB for database '%ls' finished without errors on %ls (local time). This is an informational message only; no user action is required. |
| 17656 | 10 | Yes | Warning \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\* |
| 17657 | 10 | Yes | Attempting to change default collation to %s. |
| 17658 | 10 | Yes | SQL Server started in single-user mode. This an informational message only. No user action is required. |
| [17659](../mssqlserver-17659-database-engine-error.md) | 10 | Yes | Warning: System table ID %d has been updated directly in database ID %d and cache coherence may not have been maintained. SQL Server should be restarted. |
| [17660](../mssqlserver-17660-database-engine-error.md) | 10 | Yes | Starting without recovery. This is an informational message only. No user action is required. |
| 17661 | 10 | Yes | Recovering all databases, but not clearing tempdb. This is an informational message only. No user action is required. |
| 17663 | 10 | Yes | Server name is '%s'. This is an informational message only. No user action is required. |
| 17664 | 10 | Yes | The NETBIOS name of the local node that is running the server is '%ls'. This is an informational message only. No user action is required. |
| 17674 | 10 | Yes | Login: %.\*ls %.\*ls, server process ID (SPID): %d, kernel process ID (KPID): %d. |
| [17676](../mssqlserver-17676-database-engine-error.md) | 10 | Yes | SQL Server shutdown due to Ctrl-C or Ctrl-Break signal. This is an informational message only. No user action is required. |
| 17681 | 10 | Yes | Loading default collation %s for this instance of SQL Server. |
| 17750 | 16 | Yes | Could not load the DLL %ls, or one of the DLLs it references. Reason: %ls. |
| 17751 | 16 | Yes | Could not find the function %ls in the library %ls. Reason: %ls. |
| 17752 | 16 | Yes | SQL Server has insufficient memory to run the extended stored procedure '%ls'. Release server memory resources by closing connections or ending transactions. |
| 17753 | 16 | No | %.\*ls can only be executed in the master database. |
| 17802 | 20 | Yes | The Tabular Data Stream (TDS) version 0x%x of the client library used to open the connection is unsupported or unknown. The connection has been closed. %.\*ls |
| [17803](../mssqlserver-17803-database-engine-error.md) | 20 | Yes | There was a memory allocation failure during connection establishment. Reduce nonessential memory load, or increase system memory. The connection has been closed.%.\*ls |
| 17805 | 20 | Yes | The value in the usertype field of the login record is invalid. The value 0x01, which was used by Sybase clients, is no longer supported by SQL Server. Contact the vendor of the client library that is being used to connect to SQL Server.%.\*ls |
| 17806 | 20 | Yes | SSPI handshake failed with error code 0x%x, state %d while establishing a connection with integrated security; the connection has been closed. Reason: %.\*ls %.\*ls %.\*ls |
| 17807 | 20 | Yes | Event '%ld', which was received from the client, is not recognized by SQL Server. Contact the vendor of the client library that is being used to connect to SQL Server, and have the vendor fix the event number in the tabular data stream that is sent. |
| [17809](../mssqlserver-17809-database-engine-error.md) | 20 | Yes | Could not connect because the maximum number of '%ld' user connections has already been reached. The system administrator can use sp_configure to increase the maximum value. The connection has been closed.%.\*ls |
| 17810 | 20 | Yes | Could not connect because the maximum number of '%ld' dedicated administrator connections already exists. Before a new connection can be made, the existing dedicated administrator connection must be dropped, either by logging off or ending the process.%.\*ls |
| 17811 | 10 | Yes | The maximum number of dedicated administrator connections for this instance is '%ld' |
| 17812 | 10 | Yes | Dedicated administrator connection has been disconnected. This is an informational message only. No user action is required. |
| 17813 | 20 | Yes | The requested service has been stopped or disabled and is unavailable at this time. The connection has been closed.%.\*ls |
| 17816 | 20 | No | Login to remote SQL Server failed with error %d: %.\*ls |
| 17817 | 20 | No | Unsupport login ack packet response received when opening client connection.%.\*ls |
| 17818 | 20 | No | Connection to remote SQL Server failed with error %d. |
| 17819 | 20 | No | The SQL Server or the endpoint is configured to accept only strict (TDS 8.0 and above) connections. The connection has been closed. |
| 17821 | 20 | No | A valid TLS certificate is not configured to accept strict (TDS 8.0 and above) connections. The connection has been closed. |
| 17825 | 18 | Yes | Could not close network endpoint, or could not shut down network library. The cause is an internal error in a network library. Review the error log: the entry listed after this error contains the error code from the network library. |
| [17826](../mssqlserver-17826-database-engine-error.md) | 18 | Yes | Could not start the network library because of an internal error in the network library. To determine the cause, review the errors immediately preceding this one in the error log. |
| 17827 | 20 | Yes | There was a failure while attempting to encrypt a password. The connection has been closed.%.\*ls |
| 17828 | 20 | Yes | The prelogin packet used to open the connection is structurally invalid; the connection has been closed. Please contact the vendor of the client library.%.\*ls |
| 17829 | 20 | Yes | A network error occurred while establishing a connection; the connection has been closed.%.\*ls |
| 17830 | 20 | Yes | Network error code 0x%x occurred while establishing a connection; the connection has been closed. This may have been caused by client or server login timeout expiration. Time spent during login: total %d ms, enqueued %d ms, network writes %d ms, network reads %d ms, establishing SSL %d ms, network reads during SSL %d ms, network writes during SSL %d ms, secure calls during SSL %d ms, enqueued during SSL %d ms, negotiating SSPI %d ms, network reads during SSPI %d ms, network writes during SSPI %d ms, secure calls during SSPI %d ms, enqueued during SSPI %d ms, validating login %d ms, including user-defined login processing %d ms.%.\*ls |
| [17832](../mssqlserver-17832-database-engine-error.md) | 20 | Yes | The login packet used to open the connection is structurally invalid; the connection has been closed. Please contact the vendor of the client library.%.\*ls |
| 17835 | 20 | Yes | Encryption is required to connect to this server but the client library does not support encryption; the connection has been closed. Please upgrade your client library.%.\*ls |
| 17836 | 20 | Yes | Length specified in network packet payload did not match number of bytes read; the connection has been closed. Please contact the vendor of the client library.%.\*ls |
| 17881 | 16 | Yes | '%ls' is an unsupported Open Data Services API. |
| [17883](../mssqlserver-17883-database-engine-error.md) | 10 | Yes | Process %ld:%ld:%ld (0x%lx) Worker 0x%p appears to be non-yielding on Scheduler %ld. Thread creation time: %I64d. Approx Thread CPU Used: kernel %I64d ms, user %I64d ms. Process Utilization %d%%. System Idle %d%%. Interval: %I64d ms. |
| [17884](../mssqlserver-17884-database-engine-error.md) | 10 | Yes | New queries assigned to process on Node %d have not been picked |
| 17885 | 16 | No | An unexpected query string was passed to a Web Service Description Language (WSDL) generation procedure. |
| 17886 | 20 | Yes | The server will drop the connection, because the client driver has sent multiple requests while the session is in single-user mode. This error occurs when a client sends a request to reset the connection while there are batches still running in the session, or when the client sends a request while the session is resetting a connection. Please contact the client driver vendor. |
| [17887](../mssqlserver-17887-database-engine-error.md) | 10 | Yes | IO Completion Listener (0x%lx) Worker 0x%p appears to be non-yielding on Node %ld. Approx CPU Used: kernel %I64d ms, user %I64d ms, Interval: %I64d. |
| 17888 | 10 | Yes | All schedulers on Node %d appear deadlocked due to a large number of worker threads waiting on %ls. Process Utilization %d%%. |
| 17889 | 16 | Yes | A new connection was rejected because the maximum number of connections on session ID %d has been reached. Close an existing connection on this session and retry.%.\*ls |
| [17890](../mssqlserver-17890-database-engine-error.md) | 10 | Yes | A significant part of sql server process memory has been paged out. This may result in a performance degradation. Duration: %d seconds. Working set (KB): %I64d, committed (KB): %I64d, memory utilization: %d%%. |
| 17891 | 10 | Yes | Resource Monitor (0x%lx) Worker 0x%p appears to be non-yielding on Node %ld. Memory freed: %I64d KB. Last wait: %ls. Last clerk: type %ls, name %ls. Approx CPU Used: kernel %I64d ms, user %I64d ms, Interval: %I64d. |
| [17892](../mssqlserver-17892-database-engine-error.md) | 20 | Yes | Logon failed for login '%.\*ls' due to trigger execution.%.\*ls |
| 17893 | 20 | Yes | Failed to get client host address while preparing to execute LOGON triggers. |
| 17894 | 10 | Yes | Dispatcher (0x%lx) from dispatcher pool '%.\*ls' Worker 0x%p appears to be stuck on Node %ld. Approx CPU Used: kernel %I64d ms, user %I64d ms, Interval: %I64d. |
| 17895 | 10 | Yes | sp_server_diagnostics running on Worker 0x%p appears to be non-yielding on Node %ld. |
| 17896 | 20 | Yes | The Tabular Data Stream (TDS) version 0x%x of the client library used to recover a dead connection is unsupported or unknown. The server could not recover the connection to the requested TDS version. The connection has been closed. %.\*ls |
| 17897 | 20 | Yes | Session recovery feature data used in login record to open or recover a connection is structurally or semantically invalid; the connection has been closed. Please contact the vendor of the client library.%.\*ls |
| 17898 | 16 | Yes | The Tabular Data Stream (TDS) version 0x%x of the client library used to open the connection is unsupported or unknown. Please use the client library which supports TDS Version 7.4 or higher (for example Microsoft SQL Server Native Client 11.0 or higher, ADO.NET 4.5 or higher, or Microsoft SQL Server JDBC 4.0 or higher). The connection has been closed. |
| 17899 | 16 | Yes | Login timer expired for the client connection. |
| 17900 | 20 | Yes | A network error occurred in the established connection; the connection has been closed. |
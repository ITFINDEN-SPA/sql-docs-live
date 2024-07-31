---
title: "SQL Server Event Class Reference"
description: Record events as they occur in an instance of SQL Server Database Engine by using the SQL Server Profiler.
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: reference
helpviewer_keywords:
  - "events [SQL Server], event classes"
  - "event classes [SQL Server], listed"
  - "event classes [SQL Server]"
  - "SQL Server event classes, listed"
  - "SQL Server event classes"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# SQL Server Event Class Reference
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] lets you record events as they occur in an instance of the [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. The recorded events are instances of the event classes in the trace definition. In [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], event classes and their event categories are available on the **Events Selection** tab of the **Trace File Properties** dialog box.  
  
 The following table describes the event categories and lists their associated event classes.  
  
|Event Category|Event Classes|  
|--------------------|-------------------|  
|The [Broker Event Category](../../relational-databases/event-classes/broker-event-category.md) includes event classes that are produced by the [!INCLUDE[ssSB](../../includes/sssb-md.md)].|[Broker:Activation Event Class](../../relational-databases/event-classes/broker-activation-event-class.md)<br /><br /> [Broker:Connection Event Class](../../relational-databases/event-classes/broker-connection-event-class.md)<br /><br /> [Broker:Conversation Event Class](../../relational-databases/event-classes/broker-conversation-event-class.md)<br /><br /> [Broker:Conversation Group Event Class](../../relational-databases/event-classes/broker-conversation-group-event-class.md)<br /><br /> [Broker:Corrupted Message Event Class](../../relational-databases/event-classes/broker-corrupted-message-event-class.md)<br /><br /> [Broker:Forwarded Message Dropped Event Class](../../relational-databases/event-classes/broker-forwarded-message-dropped-event-class.md)<br /><br /> [Broker:Forwarded Message Sent Event Class](../../relational-databases/event-classes/broker-forwarded-message-sent-event-class.md)<br /><br /> [Broker:Message Classify Event Class](../../relational-databases/event-classes/broker-message-classify-event-class.md)<br /><br /> [Broker:Message Drop Event Class](../../relational-databases/event-classes/broker-message-drop-event-class.md)<br /><br /> [Broker:Remote Message Ack Event Class](../../relational-databases/event-classes/broker-remote-message-ack-event-class.md)|  
|The [Cursors Event Category](../../relational-databases/event-classes/cursors-event-category.md) includes event classes that are produced by cursor operations.|[CursorClose Event Class](../../relational-databases/event-classes/cursorclose-event-class.md)<br /><br /> [CursorExecute Event Class](../../relational-databases/event-classes/cursorexecute-event-class.md)<br /><br /> [CursorImplicitConversion Event Class](../../relational-databases/event-classes/cursorimplicitconversion-event-class.md)<br /><br /> [CursorOpen Event Class](../../relational-databases/event-classes/cursoropen-event-class.md)<br /><br /> [CursorPrepare Event Class](../../relational-databases/event-classes/cursorprepare-event-class.md)<br /><br /> [CursorRecompile Event Class](../../relational-databases/event-classes/cursorrecompile-event-class.md)<br /><br /> [CursorUnprepare Event Class](../../relational-databases/event-classes/cursorunprepare-event-class.md)|  
|The [CLR Event Category](../../relational-databases/event-classes/clr-event-category.md) includes event classes that are produced by the execution of .NET common language runtime (CLR) objects.|[Assembly Load Event Class](/dotnet/api/system.appdomain.assemblyload)|  
|The [Database Event Category](../../relational-databases/event-classes/database-event-category.md) includes event classes that are produced when data or log files grow or shrink automatically.|[Data File Auto Grow Event Class](../../relational-databases/event-classes/data-file-auto-grow-event-class.md)<br /><br /> [Data File Auto Shrink Event Class](../../relational-databases/event-classes/data-file-auto-shrink-event-class.md)<br /><br /> [Database Mirroring State Change Event Class](../../relational-databases/event-classes/database-mirroring-state-change-event-class.md)<br /><br /> [Log File Auto Grow Event Class](../../relational-databases/event-classes/log-file-auto-grow-event-class.md)<br /><br /> [Log File Auto Shrink Event Class](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md)|  
|The [Deprecation Event Category](../../relational-databases/event-classes/deprecation-event-category.md) includes deprecation related events.|[Deprecation Announcement Event Class](../../relational-databases/event-classes/deprecation-announcement-event-class.md)<br /><br /> [Deprecation Final Support Event Class](../../relational-databases/event-classes/deprecation-final-support-event-class.md)|  
|The [Errors and Warnings Event Category &#40;Database Engine&#41;](../../relational-databases/event-classes/errors-and-warnings-event-category-database-engine.md) includes event classes that are produced when a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] error or warning is returned, for example, if an error occurs during the compilation of a stored procedure or an exception occurs in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Attention Event Class](../../relational-databases/event-classes/attention-event-class.md)<br /><br /> [Background Job Error Event Class](../../relational-databases/event-classes/background-job-error-event-class.md)<br /><br /> [Blocked Process Report Event Class](../../relational-databases/event-classes/blocked-process-report-event-class.md)<br /><br /> [CPU Threshold Exceeded Event Class](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)<br /><br /> [ErrorLog Event Class](../../relational-databases/event-classes/errorlog-event-class.md)<br /><br /> [EventLog Event Class](../../relational-databases/event-classes/eventlog-event-class.md)<br /><br /> [Exception Event Class](../../relational-databases/event-classes/exception-event-class.md)<br /><br /> [Exchange Spill Event Class](../../relational-databases/event-classes/exchange-spill-event-class.md)<br /><br /> [Execution Warnings Event Class](../../relational-databases/event-classes/execution-warnings-event-class.md)<br /><br /> [Hash Warning Event Class](../../relational-databases/event-classes/hash-warning-event-class.md)<br /><br /> [Missing Column Statistics Event Class](../../relational-databases/event-classes/missing-column-statistics-event-class.md)<br /><br /> [Missing Join Predicate Event Class](../../relational-databases/event-classes/missing-join-predicate-event-class.md)<br /><br /> [Sort Warnings Event Class](../../relational-databases/event-classes/sort-warnings-event-class.md)<br /><br /> [User Error Message Event Class](../../relational-databases/event-classes/user-error-message-event-class.md)|  
|The [Full Text Event Category](../../relational-databases/event-classes/full-text-event-category.md) includes event classes that are produced when full-text searches are started, interrupted, or stopped.|[FT:Crawl Aborted Event Class](../../relational-databases/event-classes/ft-crawl-aborted-event-class.md)<br /><br /> [FT:Crawl Started Event Class](../../relational-databases/event-classes/ft-crawl-started-event-class.md)<br /><br /> [FT:Crawl Stopped Event Class](../../relational-databases/event-classes/ft-crawl-stopped-event-class.md)|  
|The [Locks Event Category](../../relational-databases/event-classes/locks-event-category.md) includes event classes that are produced when a lock is acquired, cancelled, released, or has some other action performed on it.|[Deadlock Graph Event Class](../../relational-databases/event-classes/deadlock-graph-event-class.md)<br /><br /> [Lock:Acquired Event Class](../../relational-databases/event-classes/lock-acquired-event-class.md)<br /><br /> [Lock:Cancel Event Class](../../relational-databases/event-classes/lock-cancel-event-class.md)<br /><br /> [Lock:Deadlock Chain Event Class](../../relational-databases/event-classes/lock-deadlock-chain-event-class.md)<br /><br /> [Lock:Deadlock Event Class](../../relational-databases/event-classes/lock-deadlock-event-class.md)<br /><br /> [Lock:Escalation Event Class](../../relational-databases/event-classes/lock-escalation-event-class.md)<br /><br /> [Lock:Released Event Class](../../relational-databases/event-classes/lock-released-event-class.md)<br /><br /> [Lock:Timeout &#40;timeout &#62; 0&#41; Event Class](../../relational-databases/event-classes/lock-timeout-timeout-0-event-class.md)<br /><br /> [Lock:Timeout Event Class](../../relational-databases/event-classes/lock-timeout-event-class.md)|  
|The [Objects Event Category](../../relational-databases/event-classes/objects-event-category.md) includes event classes that are produced when database objects are created, opened, closed, dropped, or deleted.|[Auto Stats Event Class](../../relational-databases/event-classes/auto-stats-event-class.md)<br /><br /> [Object:Altered Event Class](../../relational-databases/event-classes/object-altered-event-class.md)<br /><br /> [Object:Created Event Class](../../relational-databases/event-classes/object-created-event-class.md)<br /><br /> [Object:Deleted Event Class](../../relational-databases/event-classes/object-deleted-event-class.md)|  
|The [OLEDB Event Category](../../relational-databases/event-classes/oledb-event-category.md) includes event classes that are produced by OLE DB calls.|[OLEDB Call Event Class](../../relational-databases/event-classes/oledb-call-event-class.md)<br /><br /> [OLEDB DataRead Event Class](../../relational-databases/event-classes/oledb-dataread-event-class.md)<br /><br /> [OLEDB Errors Event Class](../../relational-databases/event-classes/oledb-errors-event-class.md)<br /><br /> [OLEDB Provider Information Event Class](../../relational-databases/event-classes/oledb-provider-information-event-class.md)<br /><br /> [OLEDB QueryInterface Event Class](../../relational-databases/event-classes/oledb-queryinterface-event-class.md)|  
|The [Performance Event Category](../../relational-databases/event-classes/performance-event-category.md) includes event classes that are produced when SQL data manipulation language (DML) operators execute.|[Degree of Parallelism &#40;7.0 Insert&#41; Event Class](../../relational-databases/event-classes/degree-of-parallelism-7-0-insert-event-class.md)<br /><br /> [Performance Statistics Event Class](../../relational-databases/event-classes/performance-statistics-event-class.md)<br /><br /> [Showplan All Event Class](../../relational-databases/event-classes/showplan-all-event-class.md)<br /><br /> [Showplan All for Query Compile Event Class](../../relational-databases/event-classes/showplan-all-for-query-compile-event-class.md)<br /><br /> [Showplan Statistics Profile Event Class](../../relational-databases/event-classes/showplan-statistics-profile-event-class.md)<br /><br /> [Showplan Text Event Class](../../relational-databases/event-classes/showplan-text-event-class.md)<br /><br /> [Showplan Text &#40;Unencoded&#41; Event Class](../../relational-databases/event-classes/showplan-text-unencoded-event-class.md)<br /><br /> [Showplan XML Event Class](../../relational-databases/event-classes/showplan-xml-event-class.md)<br /><br /> [Showplan XML for Query Compile Event Class](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)<br /><br /> [Showplan XML Statistics Profile Event Class](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)<br /><br /> [SQL:FullTextQuery Event Class](../../relational-databases/event-classes/sql-fulltextquery-event-class.md)|  
|The [Progress Report Event Category](../../relational-databases/event-classes/progress-report-event-category.md) includes the **Progress Report: Online Index Operation** event class.|[Progress Report: Online Index Operation Event Class](../../relational-databases/event-classes/progress-report-online-index-operation-event-class.md)|  
|The [Scans Event Category](../../relational-databases/event-classes/scans-event-category.md) includes event classes that are produced when tables and indexes are scanned.|[Scan:Started Event Class](../../relational-databases/event-classes/scan-started-event-class.md)<br /><br /> [Scan:Stopped Event Class](../../relational-databases/event-classes/scan-stopped-event-class.md)|  
|The [Security Audit Event Category](../../relational-databases/event-classes/security-audit-event-category-sql-server-profiler.md) includes event classes that are used to audit server activity.|[Audit Add DB User Event Class](../../relational-databases/event-classes/audit-add-db-user-event-class.md)<br /><br /> [Audit Add Login to Server Role Event Class](../../relational-databases/event-classes/audit-add-login-to-server-role-event-class.md)<br /><br /> [Audit Add Member to DB Role Event Class](../../relational-databases/event-classes/audit-add-member-to-db-role-event-class.md)<br /><br /> [Audit Add Role Event Class](../../relational-databases/event-classes/audit-add-role-event-class.md)<br /><br /> [Audit Addlogin Event Class](../../relational-databases/event-classes/audit-addlogin-event-class.md)<br /><br /> [Audit App Role Change Password Event Class](../../relational-databases/event-classes/audit-app-role-change-password-event-class.md)<br /><br /> [Audit Backup and Restore Event Class](../../relational-databases/event-classes/audit-backup-and-restore-event-class.md)<br /><br /> [Audit Broker Conversation Event Class](../../relational-databases/event-classes/audit-broker-conversation-event-class.md)<br /><br /> [Audit Broker Login Event Class](../../relational-databases/event-classes/audit-broker-login-event-class.md)<br /><br /> [Audit Change Audit Event Class](../../relational-databases/event-classes/audit-change-audit-event-class.md)<br /><br /> [Audit Change Database Owner Event Class](../../relational-databases/event-classes/audit-change-database-owner-event-class.md)<br /><br /> [Audit Database Management Event Class](../../relational-databases/event-classes/audit-database-management-event-class.md)<br /><br /> [Audit Database Object Access Event Class](../../relational-databases/event-classes/audit-database-object-access-event-class.md)<br /><br /> [Audit Database Object GDR Event Class](../../relational-databases/event-classes/audit-database-object-gdr-event-class.md)<br /><br /> [Audit Database Object Management Event Class](../../relational-databases/event-classes/audit-database-object-management-event-class.md)<br /><br /> [Audit Database Object Take Ownership Event Class](../../relational-databases/event-classes/audit-database-object-take-ownership-event-class.md)<br /><br /> [Audit Database Operation Event Class](../../relational-databases/event-classes/audit-database-operation-event-class.md)<br /><br /> [Audit Database Principal Impersonation Event Class](../../relational-databases/event-classes/audit-database-principal-impersonation-event-class.md)<br /><br /> [Audit Database Principal Management Event Class](../../relational-databases/event-classes/audit-database-principal-management-event-class.md)<br /><br /> [Audit Database Scope GDR Event Class](../../relational-databases/event-classes/audit-database-scope-gdr-event-class.md)<br /><br /> [Audit DBCC Event Class](../../relational-databases/event-classes/audit-dbcc-event-class.md)<br /><br /> [Audit Login Change Password Event Class](../../relational-databases/event-classes/audit-login-change-password-event-class.md)<br /><br /> [Audit Login Change Property Event Class](../../relational-databases/event-classes/audit-login-change-property-event-class.md)<br /><br /> [Audit Login Event Class](../../relational-databases/event-classes/audit-login-event-class.md)<br /><br /> [Audit Login Failed Event Class](../../relational-databases/event-classes/audit-login-failed-event-class.md)<br /><br /> [Audit Login GDR Event Class](../../relational-databases/event-classes/audit-login-gdr-event-class.md)<br /><br /> [Audit Logout Event Class](../../relational-databases/event-classes/audit-logout-event-class.md)<br /><br /> [Audit Object Derived Permission Event Class](../../relational-databases/event-classes/audit-object-derived-permission-event-class.md)<br /><br /> [Audit Schema Object Access Event Class](../../relational-databases/event-classes/audit-schema-object-access-event-class.md)<br /><br /> [Audit Schema Object GDR Event Class](../../relational-databases/event-classes/audit-schema-object-gdr-event-class.md)<br /><br /> [Audit Schema Object Management Event Class](../../relational-databases/event-classes/audit-schema-object-management-event-class.md)<br /><br /> [Audit Schema Object Take Ownership Event Class](../../relational-databases/event-classes/audit-schema-object-take-ownership-event-class.md)<br /><br /> [Audit Server Alter Trace Event Class](../../relational-databases/event-classes/audit-server-alter-trace-event-class.md)<br /><br /> [Audit Server Object GDR Event Class](../../relational-databases/event-classes/audit-server-object-gdr-event-class.md)<br /><br /> [Audit Server Object Management Event Class](../../relational-databases/event-classes/audit-server-object-management-event-class.md)<br /><br /> [Audit Server Object Take Ownership Event Class](../../relational-databases/event-classes/audit-server-object-take-ownership-event-class.md)<br /><br /> [Audit Server Operation Event Class](../../relational-databases/event-classes/audit-server-operation-event-class.md)<br /><br /> [Audit Server Principal Impersonation Event Class](../../relational-databases/event-classes/audit-server-principal-impersonation-event-class.md)<br /><br /> [Audit Server Principal Management Event Class](../../relational-databases/event-classes/audit-server-principal-management-event-class.md)<br /><br /> [Audit Server Scope GDR Event Class](../../relational-databases/event-classes/audit-server-scope-gdr-event-class.md)<br /><br /> [Audit Server Starts and Stops Event Class](../../relational-databases/event-classes/audit-server-starts-and-stops-event-class.md)<br /><br /> [Audit Statement Permission Event Class](../../relational-databases/event-classes/audit-statement-permission-event-class.md)|  
|The [Server Event Category](../../relational-databases/event-classes/server-event-category.md) contains general server events.|[Mount Tape Event Class](../../relational-databases/event-classes/mount-tape-event-class.md)<br /><br /> [Server Memory Change Event Class](../../relational-databases/event-classes/server-memory-change-event-class.md)<br /><br /> [Trace File Close Event Class](../../relational-databases/event-classes/trace-file-close-event-class.md)|  
|The [Sessions Event Category](../../relational-databases/event-classes/sessions-event-category.md) includes event classes produced by clients connecting to and disconnecting from an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[ExistingConnection Event Class](../../relational-databases/event-classes/existingconnection-event-class.md)|  
|The [Stored Procedures Event Category](../../relational-databases/event-classes/stored-procedures-event-category.md) includes event classes produced by the execution of stored procedures.|[PreConnect:Completed Event Class](../../relational-databases/event-classes/preconnect-completed-event-class.md)<br /><br /> [PreConnect:Starting Event Class](../../relational-databases/event-classes/preconnect-starting-event-class.md)<br /><br /> [RPC:Completed Event Class](../../relational-databases/event-classes/rpc-completed-event-class.md)<br /><br /> [RPC Output Parameter Event Class](../../relational-databases/event-classes/rpc-output-parameter-event-class.md)<br /><br /> [RPC:Starting Event Class](../../relational-databases/event-classes/rpc-starting-event-class.md)<br /><br /> [SP:CacheHit Event Class](../../relational-databases/event-classes/sp-cachehit-event-class.md)<br /><br /> [SP:CacheInsert Event Class](../../relational-databases/event-classes/sp-cacheinsert-event-class.md)<br /><br /> [SP:CacheMiss Event Class](../../relational-databases/event-classes/sp-cachemiss-event-class.md)<br /><br /> [SP:CacheRemove Event Class](../../relational-databases/event-classes/sp-cacheremove-event-class.md)<br /><br /> [SP:Completed Event Class](../../relational-databases/event-classes/sp-completed-event-class.md)<br /><br /> [SP:Recompile Event Class](../../relational-databases/event-classes/sp-recompile-event-class.md)<br /><br /> [SP:Starting Event Class](../../relational-databases/event-classes/sp-starting-event-class.md)<br /><br /> [SP:StmtCompleted Event Class](../../relational-databases/event-classes/sp-stmtcompleted-event-class.md)<br /><br /> [SP:StmtStarting Event Class](../../relational-databases/event-classes/sp-stmtstarting-event-class.md)|  
|The [Transactions Event Category](../../relational-databases/event-classes/transactions-event-category.md) includes event classes produced by the execution of [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator transactions or by writing to the transaction log.|[DTCTransaction Event Class](../../relational-databases/event-classes/dtctransaction-event-class.md)<br /><br /> [SQLTransaction Event Class](../../relational-databases/event-classes/sqltransaction-event-class.md)<br /><br /> [TM: Begin Tran Completed Event Class](../../relational-databases/event-classes/tm-begin-tran-completed-event-class.md)<br /><br /> [TM: Begin Tran Starting Event Class](../../relational-databases/event-classes/tm-begin-tran-starting-event-class.md)<br /><br /> [TM: Commit Tran Completed Event Class](../../relational-databases/event-classes/tm-commit-tran-completed-event-class.md)<br /><br /> [TM: Commit Tran Starting Event Class](../../relational-databases/event-classes/tm-commit-tran-starting-event-class.md)<br /><br /> [TM: Promote Tran Completed Event Class](../../relational-databases/event-classes/tm-promote-tran-completed-event-class.md)<br /><br /> [TM: Promote Tran Starting Event Class](../../relational-databases/event-classes/tm-promote-tran-starting-event-class.md)<br /><br /> [TM: Rollback Tran Completed Event Class](../../relational-databases/event-classes/tm-rollback-tran-completed-event-class.md)<br /><br /> [TM: Rollback Tran Starting Event Class](../../relational-databases/event-classes/tm-rollback-tran-starting-event-class.md)<br /><br /> [TM: Save Tran Completed Event Class](../../relational-databases/event-classes/tm-save-tran-completed-event-class.md)<br /><br /> [TM: Save Tran Starting Event Class](../../relational-databases/event-classes/tm-save-tran-starting-event-class.md)<br /><br /> [TransactionLog Event Class](../../relational-databases/event-classes/transactionlog-event-class.md)|  
|The [TSQL Event Category](../../relational-databases/event-classes/tsql-event-category.md) includes event classes produced by the execution of Transact-SQL statements passed to an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] from the client.|[Exec Prepared SQL Event Class](../../relational-databases/event-classes/exec-prepared-sql-event-class.md)<br /><br /> [Prepare SQL Event Class](../../relational-databases/event-classes/prepare-sql-event-class.md)<br /><br /> [SQL:BatchCompleted Event Class](../../relational-databases/event-classes/sql-batchcompleted-event-class.md)<br /><br /> [SQL:BatchStarting Event Class](../../relational-databases/event-classes/sql-batchstarting-event-class.md)<br /><br /> [SQL:StmtCompleted Event Class](../../relational-databases/event-classes/sql-stmtcompleted-event-class.md)<br /><br /> [SQL:StmtRecompile Event Class](../../relational-databases/event-classes/sql-stmtrecompile-event-class.md)<br /><br /> [SQL:StmtStarting Event Class](../../relational-databases/event-classes/sql-stmtstarting-event-class.md)<br /><br /> [Unprepare SQL Event Class](../../relational-databases/event-classes/unprepare-sql-event-class.md)<br /><br /> [XQuery Static Type Event Class](../../relational-databases/event-classes/xquery-static-type-event-class.md)|  
|The [User-Configurable Event Category](../../relational-databases/event-classes/user-configurable-event-category.md) includes event classes that you can define.|[User-Configurable Event Class](../../relational-databases/event-classes/user-configurable-event-class.md)|  
  
## See Also  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
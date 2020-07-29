---
title: DDL 事件 | Microsoft 文件
ms.custom: ''
ms.date: 11/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL events
- DDL triggers, events
- events [SQL Server], DDL
ms.assetid: 62ef24b4-3553-4aed-b62a-670980bae501
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4281b67d44e7a1aa7404e89b07a505416f38260f
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243319"
---
# <a name="ddl-events"></a>DDL 事件
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  下表列出可用以引發 DDL 觸發程序或事件通知的 DDL 事件。 請注意，每個事件都會對應到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或預存程序，且陳述式語法已修改為在關鍵字之間加上了底線字元 (_)。  
  
> [!IMPORTANT]  
>  執行類似 DDL 作業的系統預存程序也可以引發 DDL 觸發程序和事件通知。 請測試 DDL 觸發程序和事件通知，以判斷它們對執行之系統預存程序的回應。 例如，CREATE TYPE 陳述式與 **sp_addtype** 預存程序都會引發在 CREATE_TYPE 事件上建立的 DDL 觸發程序或事件通知。  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>具有伺服器或資料庫範圍的 DDL 陳述式  
 可以建立 DDL 觸發程序或事件通知，以便在下列事件發生於此觸發程序或事件通知建立所在的資料庫內或是伺服器執行個體的任何地方時，可引發此觸發程序或事件通知來進行回應。  
  
:::row:::
    :::column:::
        CREATE_APPLICATION_ROLE (適用於 CREATE APPLICATION ROLE 陳述式與 **sp_addapprole**。 如果建立了新結構描述，此事件也會觸發 CREATE_SCHEMA 事件)。
    :::column-end:::
    :::column:::
        ALTER_APPLICATION_ROLE (適用於 ALTER APPLICATION ROLE 陳述式與 **sp_approlepassword**)。
    :::column-end:::
    :::column:::
        DROP_APPLICATION_ROLE (適用於 DROP APPLICATION ROLE 陳述式與 **sp_dropapprole**)。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ASSEMBLY
    :::column-end:::
    :::column:::
        ALTER_ASSEMBLY
    :::column-end:::
    :::column:::
        DROP_ASSEMBLY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ASYMMETRIC_KEY
    :::column-end:::
    :::column:::
        ALTER_ASYMMETRIC_KEY
    :::column-end:::
    :::column:::
        DROP_ASYMMETRIC_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER_AUTHORIZATION
    :::column-end:::
    :::column:::
        ALTER_AUTHORIZATION_DATABASE (已指定 ON DATABASE 時適用於 ALTER AUTHORIZATION 陳述式與 **sp_changedbowner**)。
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
    :::column:::
        CREATE_BROKER_PRIORITY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CERTIFICATE
    :::column-end:::
    :::column:::
        ALTER_CERTIFICATE
    :::column-end:::
    :::column:::
        DROP_CERTIFICATE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CONTRACT
    :::column-end:::
    :::column:::
        DROP_CONTRACT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CREDENTIAL
    :::column-end:::
    :::column:::
        ALTER_CREDENTIAL
    :::column-end:::
    :::column:::
        DROP_CREDENTIAL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GRANT_DATABASE
    :::column-end:::
    :::column:::
        DENY_DATABASE
    :::column-end:::
    :::column:::
        REVOKE_DATABASE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
    :::column:::
        ALTER_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
    :::column:::
        DENY_DATABASE_AUDIT_SPEFICIATION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE_ENCRYPTION_KEY
    :::column-end:::
    :::column:::
        ALTER_DATABASE_ENCRYPTION_KEY
    :::column-end:::
    :::column:::
        DROP_DATABASE_ENCRYPTION_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DEFAULT
    :::column-end:::
    :::column:::
        DROP_DEFAULT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BIND_DEFAULT (適用於 **sp_bindefault**)。
    :::column-end:::
    :::column:::
        UNBIND_DEFAULT (適用於 **sp_unbindefault**)。
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EVENT_NOTIFICATION
    :::column-end:::
    :::column:::
        DROP_EVENT_NOTIFICATION
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EXTENDED_PROPERTY (適用於 **sp_addextendedproperty**)。
    :::column-end:::
    :::column:::
        ALTER_EXTENDED_PROPERTY (適用於 **sp_updateextendedproperty**)。
    :::column-end:::
    :::column:::
        DROP_EXTENDED_PROPERTY (適用於 **sp_dropextendedproperty**)。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_CATALOG (當指定 **create** 時適用於 CREATE FULLTEXT CATALOG 陳述式和 *sp_fulltextcatalog* )。
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_CATALOG (當指定 **start_incremental** 、 *start_full*、 *Stop*或 *Rebuild*時，適用於 ALTER FULLTEXT CATALOG 陳述式、 *sp_fulltextcatalog* ，而當指定 **enable** 時，則適用於 *sp_fulltext_database* )。
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_CATALOG (當指定 **drop** 時，適用於 DROP FULLTEXT CATALOG 陳述式和 *sp_fulltextcatalog* )。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_INDEX (當指定 **create** 時，適用於 CREATE FULLTEXT INDEX 陳述式和 *sp_fulltexttable* )。
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_INDEX (當指定 **start_full** 、 *start_incremental*或 *stop*時，適用於 ALTER FULLTEXT INDEX 陳述式、 *sp_fulltextcatalog* ，而當指定了 **create**或 **drop** 以外的任何動作時，則適用於 *sp_fulltext_column* 和 *sp_fulltext_table* )。
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_INDEX (當指定 **drop** 時，適用於 DROP FULLTEXT INDEX 陳述式和 *sp_fulltexttable* )。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FULLTEXT_STOPLIST
    :::column-end:::
    :::column:::
        ALTER_FULLTEXT_STOPLIST
    :::column-end:::
    :::column:::
        DROP_FULLTEXT_STOPLIST
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_FUNCTION
    :::column-end:::
    :::column:::
        ALTER_FUNCTION
    :::column-end:::
    :::column:::
        DROP_FUNCTION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX (適用於 ALTER INDEX 陳述式和 **sp_indexoption**)。
    :::column-end:::
    :::column:::
        DROP_INDEX
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MASTER_KEY
    :::column-end:::
    :::column:::
        ALTER_MASTER_KEY
    :::column-end:::
    :::column:::
        DROP_MASTER_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MESSAGE_TYPE
    :::column-end:::
    :::column:::
        ALTER_MESSAGE_TYPE
    :::column-end:::
    :::column:::
        DROP_MESSAGE_TYPE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PARTITION_FUNCTION
    :::column-end:::
    :::column:::
        ALTER_PARTITION_FUNCTION
    :::column-end:::
    :::column:::
        DROP_PARTITION_FUNCTION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PARTITION_SCHEME
    :::column-end:::
    :::column:::
        ALTER_PARTITION_SCHEME
    :::column-end:::
    :::column:::
        DROP_PARTITION_SCHEME
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PLAN_GUIDE (適用於 **sp_create_plan_guide**)。
    :::column-end:::
    :::column:::
        ALTER_PLAN_GUIDE (當指定了 ENABLE、ENABLE ALL、DISABLE 或 DISABLE ALL 時，適用於 **sp_control_plan_guide** )。
    :::column-end:::
    :::column:::
        DROP_PLAN_GUIDE (當指定了 DROP 或 DROP ALL 時，適用於 **sp_control_plan_guide** )。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_PROCEDURE
    :::column-end:::
    :::column:::
        ALTER_PROCEDURE (適用於 ALTER PROCEDURE 陳述式和 **sp_procoption**)。
    :::column-end:::
    :::column:::
        DROP_PROCEDURE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_QUEUE
    :::column-end:::
    :::column:::
        ALTER_QUEUE
    :::column-end:::
    :::column:::
        DROP_QUEUE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_REMOTE_SERVICE_BINDING
    :::column-end:::
    :::column:::
        ALTER_REMOTE_SERVICE_BINDING
    :::column-end:::
    :::column:::
        DROP_REMOTE_SERVICE_BINDING
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SPATIAL_INDEX
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        RENAME (適用於 **sp_rename**)
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ROLE (適用於 CREATE ROLE 陳述式、 **sp_addrole**和 **sp_addgroup**)。
    :::column-end:::
    :::column:::
        ALTER_ROLE
    :::column-end:::
    :::column:::
        DROP_ROLE (適用於 DROP ROLE 陳述式、 **sp_droprole**和 **sp_dropgroup**)。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_ROLE_MEMBER
    :::column-end:::
    :::column:::
        DROP_ROLE_MEMBER
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ROUTE
    :::column-end:::
    :::column:::
        ALTER_ROUTE
    :::column-end:::
    :::column:::
        DROP_ROUTE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_RULE
    :::column-end:::
    :::column:::
        DROP_RULE
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        BIND_RULE (適用於 **sp_bindrule**)。
    :::column-end:::
    :::column:::
        UNBIND_RULE (適用於 **sp_unbindrule**)。
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SCHEMA (適用於 CREATE SCHEMA 陳述式、 **sp_addrole**、 **sp_adduser**、 **sp_addgroup**和 **sp_grantdbaccess**)。
    :::column-end:::
    :::column:::
        ALTER_SCHEMA (適用於 ALTER SCHEMA 陳述式和 **sp_changeobjectowner**)。
    :::column-end:::
    :::column:::
        DROP_SCHEMA
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SEARCH_PROPERTY_LIST
    :::column-end:::
    :::column:::
        ALTER_SEARCH_PROPERTY_LIST
    :::column-end:::
    :::column:::
        DROP_SEARCH_PROPERTY_LIST
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
    :::column:::
        CREATE_SEQUENCE_EVENTS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_ROLE
    :::column-end:::
    :::column:::
        ALTER_SERVER_ROLE
    :::column-end:::
    :::column:::
        DROP_SERVER_ROLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVICE
    :::column-end:::
    :::column:::
        ALTER_SERVICE
    :::column-end:::
    :::column:::
        DROP_SERVICE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ALTER_SERVICE_MASTER_KEY
    :::column-end:::
    :::column:::
        BACKUP_SERVICE_MASTER_KEY
    :::column-end:::
    :::column:::
        RESTORE_SERVICE_MASTER_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SIGNATURE (用於非結構描述範圍物件上的簽章作業；資料庫、組件、觸發程序)
    :::column-end:::
    :::column:::
        DROP_SIGNATURE
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SIGNATURE_SCHEMA_OBJECT (用於結構描述範圍物件；預存程序、函數)
    :::column-end:::
    :::column:::
        DROP_SIGNATURE_SCHEMA_OBJECT
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SPATIAL_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX 可用於空間索引。
    :::column-end:::
    :::column:::
        DROP_INDEX 可用於空間索引。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_STATISTICS
    :::column-end:::
    :::column:::
        DROP_STATISTICS
    :::column-end:::
    :::column:::
        UPDATE_STATISTICS
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SYMMETRIC_KEY
    :::column-end:::
    :::column:::
        ALTER_SYMMETRIC_KEY
    :::column-end:::
    :::column:::
        DROP_SYMMETRIC_KEY
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SYNONYM
    :::column-end:::
    :::column:::
        DROP_SYNONYM
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TABLE
    :::column-end:::
    :::column:::
        ALTER_TABLE (適用於 ALTER TABLE 陳述式和 **sp_tableoption**)。
    :::column-end:::
    :::column:::
        DROP_TABLE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TRIGGER
    :::column-end:::
    :::column:::
        ALTER_TRIGGER (適用於 ALTER TRIGGER 陳述式和 **sp_settriggerorder**)。
    :::column-end:::
    :::column:::
        DROP_TRIGGER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_TYPE (適用於 CREATE TYPE 陳述式和 **sp_addtype**)。
    :::column-end:::
    :::column:::
        DROP_TYPE (適用於 DROP TYPE 陳述式和 **sp_droptype**)。
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_USER (適用於 CREATE USER 陳述式、 **sp_adduser**和 **sp_grantdbaccess**)。
    :::column-end:::
    :::column:::
        ALTER_USER (適用於 ALTER USER 陳述式和 **sp_change_users_login**)。
    :::column-end:::
    :::column:::
        DROP_USER (適用於 DROP USER 陳述式、 **sp_dropuser**和 **sp_revokedbaccess**)。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_VIEW
    :::column-end:::
    :::column:::
        ALTER_VIEW
    :::column-end:::
    :::column:::
        DROP_VIEW
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_XML_INDEX
    :::column-end:::
    :::column:::
        ALTER_INDEX 可用於 XML 索引。
    :::column-end:::
    :::column:::
        DROP_INDEX 可用於 XML 索引。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_XML_SCHEMA_COLLECTION
    :::column-end:::
    :::column:::
        ALTER_XML_SCHEMA_COLLECTION
    :::column-end:::
    :::column:::
        DROP_XML_SCHEMA_COLLECTION
    :::column-end:::
:::row-end:::
 
## <a name="ddl-statements-that-have-server-scope"></a>具有伺服器範圍的 DDL 陳述式  
 可以建立 DDL 觸發程序或事件通知，以便在伺服器執行個體的任何地方發生下列事件時，引發該觸發程序或事件通知來加以回應。  
  
:::row:::
    :::column:::
        ALTER_AUTHORIZATION_SERVER
    :::column-end:::
    :::column:::
        ALTER_SERVER_CONFIGURATION
    :::column-end:::
    :::column:::
        ALTER_INSTANCE (當指定本機伺服器執行個體時，適用於 **sp_configure** 和 **sp_addserver** )。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_AVAILABILITY_GROUP
    :::column-end:::
    :::column:::
        ALTER_AVAILABILITY_GROUP
    :::column-end:::
    :::column:::
        DROP_AVAILABILITY_GROUP
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CREDENTIAL
    :::column-end:::
    :::column:::
        ALTER_CREDENTIAL
    :::column-end:::
    :::column:::
        DROP_CREDENTIAL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
    :::column:::
        ALTER_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
    :::column:::
        DROP_CRYPTOGRAPHIC_PROVIDER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_DATABASE
    :::column-end:::
    :::column:::
        ALTER_DATABASE (適用於 ALTER DATABASE 陳述式和 **sp_fulltext_database**)。
    :::column-end:::
    :::column:::
        DROP_DATABASE
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_ENDPOINT
    :::column-end:::
    :::column:::
        ALTER_ENDPOINT
    :::column-end:::
    :::column:::
        DROP_ENDPOINT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EVENT_SESSION
    :::column-end:::
    :::column:::
        ALTER_EVENT_SESSION
    :::column-end:::
    :::column:::
        DROP_EVENT_SESSION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_EXTENDED_PROCEDURE (適用於 **sp_addextendedproc**)。
    :::column-end:::
    :::column:::
        DROP_EXTENDED_PROCEDURE (適用於 **sp_dropextendedproc**)。
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LINKED_SERVER (適用於 **sp_addlinkedserver**)。
    :::column-end:::
    :::column:::
        ALTER_LINKED_SERVER (適用於 **sp_serveroption**)。
    :::column-end:::
    :::column:::
        DROP_LINKED_SERVER (當指定連結伺服器時，適用於 **sp_dropserver** )。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LINKED_SERVER_LOGIN (適用於 **sp_addlinkedsrvlogin**)。
    :::column-end:::
    :::column:::
        DROP_LINKED_SERVER_LOGIN (適用於 **sp_droplinkedsrvlogin**)。
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_LOGIN (當用於必須隱含建立的不存在登入時，適用於 CREATE LOGIN 陳述式、 **sp_addlogin**、 **sp_grantlogin**、 **xp_grantlogin**和 **sp_denylogin** )。
    :::column-end:::
    :::column:::
        ALTER_LOGIN (當指定 **Auto_Fix**時，適用於 ALTER LOGIN 陳述式、 **sp_defaultdb**、 **sp_defaultlanguage**、 **sp_password** 和 *sp_change_users_login* )。
    :::column-end:::
    :::column:::
        DROP_LOGIN (適用於 DROP LOGIN 陳述式、 **sp_droplogin**、 **sp_revokelogin**和 **xp_revokelogin**)。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_MESSAGE (適用於 **sp_addmessage**)。
    :::column-end:::
    :::column:::
        ALTER_MESSAGE (適用於 **sp_altermessage**)。
    :::column-end:::
    :::column:::
        DROP_MESSAGE (適用於 **sp_dropmessage**)。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_REMOTE_SERVER (適用於 **sp_addserver**)。
    :::column-end:::
    :::column:::
        ALTER_REMOTE_SERVER (適用於 **sp_setnetname**)。
    :::column-end:::
    :::column:::
        DROP_REMOTE_SERVER (當指定遠端伺服器時，適用於 **sp_dropserver** )。
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_RESOURCE_POOL
    :::column-end:::
    :::column:::
        ALTER_RESOURCE_POOL
    :::column-end:::
    :::column:::
        DROP_RESOURCE_POOL
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        GRANT_SERVER
    :::column-end:::
    :::column:::
        DENY_SERVER
    :::column-end:::
    :::column:::
        REVOKE_SERVER
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        ADD_SERVER_ROLE_MEMBER
    :::column-end:::
    :::column:::
        DROP_SERVER_ROLE_MEMBER
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_AUDIT
    :::column-end:::
    :::column:::
        ALTER_SERVER_AUDIT
    :::column-end:::
    :::column:::
        DROP_SERVER_AUDIT
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        ALTER_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
    :::column:::
        DROP_SERVER_AUDIT_SPECIFICATION
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        CREATE_WORKLOAD_GROUP
    :::column-end:::
    :::column:::
        ALTER_WORKLOAD_GROUP
    :::column-end:::
    :::column:::
        DROP_WORKLOAD_GROUP
    :::column-end:::
:::row-end:::
 
## <a name="see-also"></a>另請參閱  
 [DDL 觸發程序](../../relational-databases/triggers/ddl-triggers.md)   
 [事件通知](../../relational-databases/service-broker/event-notifications.md)   
 [DDL 事件群組](../../relational-databases/triggers/ddl-event-groups.md)  
  
  

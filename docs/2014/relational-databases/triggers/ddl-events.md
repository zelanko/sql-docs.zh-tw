---
title: DDL 事件 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: c9c90dbb072ace600258edfb4ff13f99ecadf188
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "68196516"
---
# <a name="ddl-events"></a>DDL 事件
  下表列出可用以引發 DDL 觸發程序或事件通知的 DDL 事件。 請注意，每個事件都會對應到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或預存程序，且陳述式語法已修改為在關鍵字之間加上了底線字元 (_)。  
  
> [!IMPORTANT]  
>  執行類似 DDL 作業的系統預存程序也可以引發 DDL 觸發程序和事件通知。 請測試 DDL 觸發程序和事件通知，以判斷它們對執行之系統預存程序的回應。 例如，CREATE TYPE 陳述式與 **sp_addtype** 預存程序都會引發在 CREATE_TYPE 事件上建立的 DDL 觸發程序或事件通知。  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>具有伺服器或資料庫範圍的 DDL 陳述式  
 可以建立 DDL 觸發程序或事件通知，以便在下列事件發生於此觸發程序或事件通知建立所在的資料庫內或是伺服器執行個體的任何地方時，可引發此觸發程序或事件通知來進行回應。  
  
||||  
|-|-|-|  
|CREATE_APPLICATION_ROLE (適用於 CREATE APPLICATION ROLE 陳述式與 **sp_addapprole**。 如果建立了新結構描述，此事件也會觸發 CREATE_SCHEMA 事件)。|ALTER_APPLICATION_ROLE (適用於 ALTER APPLICATION ROLE 陳述式與 **sp_approlepassword**)。|DROP_APPLICATION_ROLE (適用於 DROP APPLICATION ROLE 陳述式與 **sp_dropapprole**)。|  
|CREATE_ASSEMBLY|ALTER_ASSEMBLY|DROP_ASSEMBLY|  
|CREATE_ASYMMETRIC_KEY|ALTER_ASYMMETRIC_KEY|DROP_ASYMMETRIC_KEY|  
|ALTER_AUTHORIZATION|ALTER_AUTHORIZATION_DATABASE (已指定 ON DATABASE 時適用於 ALTER AUTHORIZATION 陳述式與 **sp_changedbowner**)。||  
|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|  
|CREATE_CERTIFICATE|ALTER_CERTIFICATE|DROP_CERTIFICATE|  
|CREATE_CONTRACT|DROP_CONTRACT||  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|GRANT_DATABASE|DENY_DATABASE|REVOKE_DATABASE|  
|CREATE_DATABASE_AUDIT_SPEFICIATION|ALTER_DATABASE_AUDIT_SPEFICIATION|DENY_DATABASE_AUDIT_SPEFICIATION|  
|CREATE_DATABASE_ENCRYPTION_KEY|ALTER_DATABASE_ENCRYPTION_KEY|DROP_DATABASE_ENCRYPTION_KEY|  
|CREATE_DEFAULT|DROP_DEFAULT||  
|BIND_DEFAULT (適用於 **sp_bindefault**)。|UNBIND_DEFAULT (適用於 **sp_unbindefault**)。||  
|CREATE_EVENT_NOTIFICATION|DROP_EVENT_NOTIFICATION||  
|CREATE_EXTENDED_PROPERTY (適用於 **sp_addextendedproperty**)。|ALTER_EXTENDED_PROPERTY (適用於 **sp_updateextendedproperty**)。|DROP_EXTENDED_PROPERTY (適用於 **sp_dropextendedproperty**)。|  
|CREATE_FULLTEXT_CATALOG (當指定 **create** 時適用於 CREATE FULLTEXT CATALOG 陳述式和 *sp_fulltextcatalog* )。|ALTER_FULLTEXT_CATALOG (當指定 **start_incremental** 、 *start_full*、 *Stop*或 *Rebuild*時，適用於 ALTER FULLTEXT CATALOG 陳述式、 *sp_fulltextcatalog* ，而當指定 **enable** 時，則適用於 *sp_fulltext_database* )。|DROP_FULLTEXT_CATALOG (當指定 **drop** 時，適用於 DROP FULLTEXT CATALOG 陳述式和 *sp_fulltextcatalog* )。|  
|CREATE_FULLTEXT_INDEX (當指定 **create** 時，適用於 CREATE FULLTEXT INDEX 陳述式和 *sp_fulltexttable* )。|ALTER_FULLTEXT_INDEX (當指定 **start_full** 、 *start_incremental*或 *stop*時，適用於 ALTER FULLTEXT INDEX 陳述式、 *sp_fulltextcatalog* ，而當指定了 **create**或 **drop** 以外的任何動作時，則適用於 *sp_fulltext_column* 和 *sp_fulltext_table* )。|DROP_FULLTEXT_INDEX (當指定 **drop** 時，適用於 DROP FULLTEXT INDEX 陳述式和 *sp_fulltexttable* )。|  
|CREATE_FULLTEXT_STOPLIST|ALTER_FULLTEXT_STOPLIST|DROP_FULLTEXT_STOPLIST|  
|CREATE_FUNCTION|ALTER_FUNCTION|DROP_FUNCTION|  
|CREATE_INDEX|ALTER_INDEX (適用於 ALTER INDEX 陳述式和 **sp_indexoption**)。|DROP_INDEX|  
|CREATE_MASTER_KEY|ALTER_MASTER_KEY|DROP_MASTER_KEY|  
|CREATE_MESSAGE_TYPE|ALTER_MESSAGE_TYPE|DROP_MESSAGE_TYPE|  
|CREATE_PARTITION_FUNCTION|ALTER_PARTITION_FUNCTION|DROP_PARTITION_FUNCTION|  
|CREATE_PARTITION_SCHEME|ALTER_PARTITION_SCHEME|DROP_PARTITION_SCHEME|  
|CREATE_PLAN_GUIDE (適用於 **sp_create_plan_guide**)。|ALTER_PLAN_GUIDE (當指定了 ENABLE、ENABLE ALL、DISABLE 或 DISABLE ALL 時，適用於 **sp_control_plan_guide** )。|DROP_PLAN_GUIDE (當指定了 DROP 或 DROP ALL 時，適用於 **sp_control_plan_guide** )。|  
|CREATE_PROCEDURE|ALTER_PROCEDURE (適用於 ALTER PROCEDURE 陳述式和 **sp_procoption**)。|DROP_PROCEDURE|  
|CREATE_QUEUE|ALTER_QUEUE|DROP_QUEUE|  
|CREATE_REMOTE_SERVICE_BINDING|ALTER_REMOTE_SERVICE_BINDING|DROP_REMOTE_SERVICE_BINDING|  
|CREATE_SPATIAL_INDEX|||  
|RENAME (適用於 **sp_rename**)|||  
|CREATE_ROLE (適用於 CREATE ROLE 陳述式、 **sp_addrole**和 **sp_addgroup**)。|ALTER_ROLE|DROP_ROLE (適用於 DROP ROLE 陳述式、 **sp_droprole**和 **sp_dropgroup**)。|  
|ADD_ROLE_MEMBER|DROP_ROLE_MEMBER||  
|CREATE_ROUTE|ALTER_ROUTE|DROP_ROUTE|  
|CREATE_RULE|DROP_RULE||  
|BIND_RULE (適用於 **sp_bindrule**)。|UNBIND_RULE (適用於 **sp_unbindrule**)。||  
|CREATE_SCHEMA (適用於 CREATE SCHEMA 陳述式、 **sp_addrole**、 **sp_adduser**、 **sp_addgroup**和 **sp_grantdbaccess**)。|ALTER_SCHEMA (適用於 ALTER SCHEMA 陳述式和 **sp_changeobjectowner**)。|DROP_SCHEMA|  
|CREATE_SEARCH_PROPERTY_LIST|ALTER_SEARCH_PROPERTY_LIST|DROP_SEARCH_PROPERTY_LIST|  
|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|  
|CREATE_SERVER_ROLE|ALTER_SERVER_ROLE|DROP_SERVER_ROLE|  
|CREATE_SERVICE|ALTER_SERVICE|DROP_SERVICE|  
|ALTER_SERVICE_MASTER_KEY|BACKUP_SERVICE_MASTER_KEY|RESTORE_SERVICE_MASTER_KEY|  
|ADD_SIGNATURE (用於非結構描述範圍物件上的簽章作業；資料庫、組件、觸發程序)|DROP_SIGNATURE||  
|ADD_SIGNATURE_SCHEMA_OBJECT (用於結構描述範圍物件；預存程序、函數)|DROP_SIGNATURE_SCHEMA_OBJECT||  
|CREATE_SPATIAL_INDEX|ALTER_INDEX 可用於空間索引。|DROP_INDEX 可用於空間索引。|  
|CREATE_STATISTICS|DROP_STATISTICS|UPDATE_STATISTICS|  
|CREATE_SYMMETRIC_KEY|ALTER_SYMMETRIC_KEY|DROP_SYMMETRIC_KEY|  
|CREATE_SYNONYM|DROP_SYNONYM||  
|CREATE_TABLE|ALTER_TABLE (適用於 ALTER TABLE 陳述式和 **sp_tableoption**)。|DROP_TABLE|  
|CREATE_TRIGGER|ALTER_TRIGGER (適用於 ALTER TRIGGER 陳述式和 **sp_settriggerorder**)。|DROP_TRIGGER|  
|CREATE_TYPE (適用於 CREATE TYPE 陳述式和 **sp_addtype**)。|DROP_TYPE (適用於 DROP TYPE 陳述式和 **sp_droptype**)。||  
|CREATE_USER (適用於 CREATE USER 陳述式、 **sp_adduser**和 **sp_grantdbaccess**)。|ALTER_USER (適用於 ALTER USER 陳述式和 **sp_change_users_login**)。|DROP_USER (適用於 DROP USER 陳述式、 **sp_dropuser**和 **sp_revokedbaccess**)。|  
|CREATE_VIEW|ALTER_VIEW|DROP_VIEW|  
|CREATE_XML_INDEX|ALTER_INDEX 可用於 XML 索引。|DROP_INDEX 可用於 XML 索引。|  
|CREATE_XML_SCHEMA_COLLECTION|ALTER_XML_SCHEMA_COLLECTION|DROP_XML_SCHEMA_COLLECTION|  
  
## <a name="ddl-statements-that-have-server-scope"></a>具有伺服器範圍的 DDL 陳述式  
 可以建立 DDL 觸發程序或事件通知，以便在伺服器執行個體的任何地方發生下列事件時，引發該觸發程序或事件通知來加以回應。  
  
||||  
|-|-|-|  
|ALTER_AUTHORIZATION_SERVER|ALTER_SERVER_CONFIGURATION|ALTER_INSTANCE (當指定本機伺服器執行個體時，適用於 **sp_configure** 和 **sp_addserver** )。|  
|CREATE_AVAILABILITY_GROUP|ALTER_AVAILABILITY_GROUP|DROP_AVAILABILITY_GROUP|  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|CREATE_CRYPTOGRAPHIC_PROVIDER|ALTER_CRYPTOGRAPHIC_PROVIDER|DROP_CRYPTOGRAPHIC_PROVIDER|  
|CREATE_DATABASE|ALTER_DATABASE (適用於 ALTER DATABASE 陳述式和 **sp_fulltext_database**)。|DROP_DATABASE|  
|CREATE_ENDPOINT|ALTER_ENDPOINT|DROP_ENDPOINT|  
|CREATE_EVENT_SESSION|ALTER_EVENT_SESSION|DROP_EVENT_SESSION|  
|CREATE_EXTENDED_PROCEDURE (適用於 **sp_addextendedproc**)。|DROP_EXTENDED_PROCEDURE (適用於 **sp_dropextendedproc**)。||  
|CREATE_LINKED_SERVER (適用於 **sp_addlinkedserver**)。|ALTER_LINKED_SERVER (適用於 **sp_serveroption**)。|DROP_LINKED_SERVER (當指定連結伺服器時，適用於 **sp_dropserver** )。|  
|CREATE_LINKED_SERVER_LOGIN (適用於 **sp_addlinkedsrvlogin**)。|DROP_LINKED_SERVER_LOGIN (適用於 **sp_droplinkedsrvlogin**)。||  
|CREATE_LOGIN (當用於必須隱含建立的不存在登入時，適用於 CREATE LOGIN 陳述式、 **sp_addlogin**、 **sp_grantlogin**、 **xp_grantlogin**和 **sp_denylogin** )。|ALTER_LOGIN (當指定 **Auto_Fix**時，適用於 ALTER LOGIN 陳述式、 **sp_defaultdb**、 **sp_defaultlanguage**、 **sp_password** 和 *sp_change_users_login* )。|DROP_LOGIN (適用於 DROP LOGIN 陳述式、 **sp_droplogin**、 **sp_revokelogin**和 **xp_revokelogin**)。|  
|CREATE_MESSAGE (適用於 **sp_addmessage**)。|ALTER_MESSAGE (適用於 **sp_altermessage**)。|DROP_MESSAGE (適用於 **sp_dropmessage**)。|  
|CREATE_REMOTE_SERVER (適用於 **sp_addserver**)。|ALTER_REMOTE_SERVER (適用於 **sp_setnetname**)。|DROP_REMOTE_SERVER (當指定遠端伺服器時，適用於 **sp_dropserver** )。|  
|CREATE_RESOURCE_POOL|ALTER_RESOURCE_POOL|DROP_RESOURCE_POOL|  
|GRANT_SERVER|DENY_SERVER|REVOKE_SERVER|  
|ADD_SERVER_ROLE_MEMBER|DROP_SERVER_ROLE_MEMBER||  
|CREATE_SERVER_AUDIT|ALTER_SERVER_AUDIT|DROP_SERVER_AUDIT|  
|CREATE_SERVER_AUDIT_SPECIFICATION|ALTER_SERVER_AUDIT_SPECIFICATION|DROP_SERVER_AUDIT_SPECIFICATION|  
|CREATE_WORKLOAD_GROUP|CREATE_WORKLOAD_GROUP|CREATE_WORKLOAD_GROUP|  
  
## <a name="see-also"></a>另請參閱  
 [DDL 觸發程序](ddl-triggers.md)   
 [事件通知](../service-broker/event-notifications.md)   
 [DDL 事件群組](ddl-event-groups.md)  
  
  

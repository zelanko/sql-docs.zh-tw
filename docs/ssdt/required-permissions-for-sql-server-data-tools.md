---
title: 必要權限
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: b27038c4-94ab-449c-90b7-29d87ce37a8b
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.openlocfilehash: fbe44c84b2a1974981dff5173015ecf0fc5e74b5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75256989"
---
# <a name="required-permissions-for-sql-server-data-tools"></a>SQL Server Data Tools 的必要權限

在 Visual Studio 中若要對資料庫執行動作，您用來登入的帳戶必須對該資料庫具備特定的權限。 依您想要執行的動作而定，所需的特定權限將有所不同。 下列各節將描述您可能會執行的每一個動作，以及執行該動作所需要的特定權限。  
  
-   [建立或部署資料庫時的權限](#DatabaseCreationAndDeploymentPermissions)  
  
-   [重構資料庫時的權限](#DatabaseRefactoringPermissions)  
  
-   [對 SQL Server 資料庫執行單元測試時的權限](#DatabaseUnitTestingPermissions)  
  
-   [產生資料時的權限](#DataGenerationPermissions)  
  
-   [比較結構描述和資料時的權限](#SchemaAndDataComparePermissions)  
  
-   [執行 Transact-SQL 編輯器時的權限](#Transact-SQLEditorPermissions)  
  
-   [SQL Server 通用語言執行平台 (SQL CLR) 專案方面的權限](#SQLCLRPermissions)  
  
## <a name="DatabaseCreationAndDeploymentPermissions"></a>建立或部署資料庫時的權限  
您必須具備下列權限，才能建立或部署資料庫。  
  
|||  
|-|-|  
|動作|必要權限|  
|匯入資料庫物件和設定|您必須能夠連接至來源資料庫。<br /><br />如果來源資料庫以 SQL Server 2005 為基礎，您還必須擁有每一個物件或對其具備 **VIEW DEFINITION** 權限。<br /><br />如果來源資料庫以 SQL Server 2008 或更新版本為基礎，您還必須擁有每一個物件或對其具備 **VIEW DEFINITION** 權限。 您的登入必須具備 **VIEW SERVER STATE** 權限 (用於資料庫加密金鑰)。|  
|匯入伺服器物件和設定|您必須能夠連接至指定的伺服器上的 master 資料庫。<br /><br />如果伺服器執行 SQL Server 2005，您必須對該伺服器具備 **VIEW ANY DEFINITION** 權限。<br /><br />如果來源資料庫以 SQL Server 2008 或更新版本為基礎，您必須對伺服器具備 **VIEW ANY DEFINITION** 權限。 您的登入必須具備 **VIEW SERVER STATE** 權限 (用於資料庫加密金鑰)。|  
|建立或更新資料庫專案|您不需要有任何的資料庫權限，就能建立或修改資料庫專案。|  
|部署新的資料庫或在已設定 [永遠重新建立資料庫]  選項的情況下部署|您必須對目標伺服器具備 **CREATE DATABASE** 權限或是其 **dbcreator** 角色的成員。<br /><br />當您建立資料庫時，Visual Studio 會連接至 model 資料庫並複製此資料庫的內容。 用以連線到目標資料庫的初始登入 (例如 *yourLogin*) 必須具備 **db_creator** 和 **CONNECT SQL** 權限。 此登入必須在 model 資料庫上已有使用者對應。 如果您具備 **sysadmin** 權限，即可藉由發出下列 Transact\-SQL 陳述式以建立對應：<br /><br />`USE [model] CREATE USER yourUser FROM LOGIN yourLogin`<br /><br />使用者 (在本例中為 yourUser) 必須對模型資料庫具備 **CONNECT** 和 **VIEW DEFINITION** 權限。 如果您具備 **sysadmin** 權限，即可藉由發出下列 Transact\-SQL 陳述式以授與這些權限：<br /><br />`USE [model] GRANT CONNECT to yourUser GRANT VIEW DEFINITION TO yourUser`<br /><br />如果部署的資料庫包含未命名的限制式並已啟用 **CheckNewContraints** 選項 (預設為啟用)，您必須具備 **db_owner** 或 **sysadmin** 權限，否則部署將會失敗。 這只限於有未命名的條件約束時才會發生。 如需 **CheckNewConstraints** 選項的詳細資訊，請參閱[資料庫專案設定](../ssdt/database-project-settings.md)。|  
|將更新部署至現有的資料庫|您必須是有效的資料庫使用者。 您也必須是 **db_ddladmin** 角色的成員、擁有結構描述，或者擁有目標資料庫上您想要建立或修改的物件。 在預先部署或部署後指令碼中運用更進階的概念 (例如登入或連結的伺服器) 時，您還需要額外的權限。<br /><br />**注意：** 如果部署至 master 資料庫，您也必須對部署的目標伺服器具備 **VIEW ANY DEFINITION** 權限。|  
|在資料庫專案中搭配 EXTERNAL_ACCESS 選項使用組件|您必須為資料庫專案設定 TRUSTWORTHY 屬性。 您的 SQL Server 登入必須具備 EXTERNAL ACCESS ASSEMBLY 權限。|  
|將組件部署至新資料庫或現有的資料庫|您必須是目標部署伺服器上 sysadmin 角色的成員。|  
  
如需詳細資訊，請參閱《SQL Server 線上叢書》。  
  
## <a name="DatabaseRefactoringPermissions"></a>重構資料庫時的權限  
「資料庫重構」  僅發生在資料庫專案內。 您必須具備使用資料庫專案方面的權限。 對於目標資料庫，只有當您將變更部署至其中時才需要相關權限。  
  
## <a name="DatabaseUnitTestingPermissions"></a>對 SQL Server 資料庫執行單元測試時的權限  
您必須具備下列權限，才能對資料庫執行單元測試。  
  
|||  
|-|-|  
|動作|必要權限|  
|執行測試動作|您必須使用執行內容資料庫連接。 如需詳細資訊，請參閱[連接字串和權限概觀](../ssdt/overview-of-connection-strings-and-permissions.md)。|  
|執行測試前或測試後動作|您必須使用有權限的內容資料庫連接。 這種資料庫連接比執行內容連接具備更多的權限。|  
|執行 TestInitialize 和 TestCleanup 指令碼|您必須使用有權限的內容資料庫連接。|  
|在執行測試之前部署資料庫變更|您必須使用有權限的內容資料庫連接。 如需詳細資訊，請參閱[如何：設定 SQL Server 單元測試執行](../ssdt/how-to-configure-sql-server-unit-test-execution.md)。|  
|在執行測試之前產生資料|您必須使用有權限的內容資料庫連接。 如需詳細資訊，請參閱[如何：設定 SQL Server 單元測試執行](../ssdt/how-to-configure-sql-server-unit-test-execution.md)。|  
  
## <a name="DataGenerationPermissions"></a>產生資料時的權限  
您必須對目標資料庫中的物件具備 **INSERT** 和 **SELECT** 權限，才能使用資料產生器產生測試資料。 如果您在產生資料之前清除資料，則也必須對目標資料庫中的物件具備 **DELETE** 權限。 如果要重設資料表的 [識別]  欄位，您必須擁有該資料表或者是 db_owner 或 db_ddladmin 角色的成員。  
  
## <a name="SchemaAndDataComparePermissions"></a>比較結構描述和資料時的權限  
您必須具備下列權限，才能比較結構描述或資料。  
  
|||  
|-|-|  
|動作|必要權限|  
|比較兩個資料庫的結構描述|您必須依[建立或部署資料庫時的權限](#DatabaseCreationAndDeploymentPermissions)中所述，具備從資料庫匯入物件和設定的權限。|  
|比較資料庫與資料庫專案的結構描述|您必須依[建立或部署資料庫時的權限](#DatabaseCreationAndDeploymentPermissions)中所述，具備從資料庫匯入物件和設定的權限。 您也必須在 Visual Studio 中開啟資料庫專案。|  
|將更新寫入目標資料庫|您必須依[建立或部署資料庫時的權限](#DatabaseCreationAndDeploymentPermissions)中所述，具備將更新部署至目標資料庫的權限。|  
|比較兩個資料庫的資料|除了比較兩個資料庫的結構描述所需的權限，您還必須對想要比較的所有資料表具備 **SELECT** 權限，再加上 **VIEW DATABASE STATE** 權限。|  
  
如需詳細資訊，請參閱《SQL Server 線上叢書》。  
  
## <a name="Transact-SQLEditorPermissions"></a>執行 Transact\-SQL 編輯器時的權限  
您能夠在 Transact\-SQL 編輯器內執行的作業取決於對目標資料庫的執行內容而定。  
  
## <a name="SQLCLRPermissions"></a>SQL Server 通用語言執行平台專案方面的權限  
下表列出部署或偵錯 CLR 專案時所需的權限：  
  
|動作|必要權限|  
|-----------|------------------------|  
|safe 權限集合組件的部署 (初始或累加)|db_DDLAdmin - 此權限將針對您所部署的組件及物件類型授與 CREATE 和 ALTER 權限<br /><br />資料庫層級 VIEW DEFINITION - 部署時所需之權限<br /><br />資料庫層級 CONNECT - 授與連接至資料庫的能力|  
|部署 external_access 權限集合組件|db_DDLAdmin - 此權限將針對您所部署的組件及物件類型授與 CREATE 和 ALTER 權限<br /><br />資料庫層級 VIEW DEFINITION - 部署時所需之權限<br /><br />資料庫層級 CONNECT - 授與連接至資料庫的能力<br /><br />此外也必須符合以下條件：<br /><br />將 TRUSTWORTHY 資料庫選項設定為 ON<br /><br />部署時所使用的登入必須具備 External Access Assembly 伺服器權限|  
|部署 unsafe 權限集合組件|db_DDLAdmin - 此權限將針對您所部署的組件及物件類型授與 CREATE 和 ALTER 權限<br /><br />資料庫層級 VIEW DEFINITION - 部署時所需之權限<br /><br />資料庫層級 CONNECT - 授與連接至資料庫的能力<br /><br />此外也必須符合以下條件：<br /><br />將 TRUSTWORTHY 資料庫選項設定為 ON<br /><br />部署時所使用的登入必須具備 Unsafe Assembly 伺服器權限|  
|遠端偵錯 SQL CLR 組件|必須具備 sysadmin 固定角色權限|  
  
> [!IMPORTANT]  
> 無論何種情況，組件擁有者都必須是您用來部署組件的使用者，或擁有者必須是該使用者隸屬為成員的角色。 此需求也適用於由您部署的組件所參考的任何組件。  
  
## <a name="see-also"></a>另請參閱  
[建立和定義 SQL Server 單元測試](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server Data Tools](../ssdt/sql-server-data-tools.md)  
  

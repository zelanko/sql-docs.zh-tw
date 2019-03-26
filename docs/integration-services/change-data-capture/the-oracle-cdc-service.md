---
title: Oracle CDC 服務 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 47759ddc-358d-405b-acb9-189ada76ea6d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 34f86e859bb09e6b3e62d9819c13ba1bf7abec26
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58276084"
---
# <a name="the-oracle-cdc-service"></a>Oracle CDC 服務
  Oracle CDC 服務是執行 xdbcdcsvc.exe 程式的一種 Windows 服務。 Oracle CDC 服務可設定為在相同電腦上執行多個 Windows 服務，每一個服務都有不同的 Windows 服務名稱。 在單一電腦上建立多個 Oracle CDC Windows 服務通常是為了在服務之間達成更好的分隔效果，或是在每一個服務需要搭配不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體使用時。  
  
 Oracle CDC 服務是使用 Oracle CDC 服務組態主控台所建立，或是透過 xdbcdcsvc.exe 程式所內建的命令列介面所定義。 在這兩個情況下，每一個建立的 Oracle CDC 服務都會與單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體有關聯 (可能會利用 **AlwaysOn** 設定進行叢集或鏡像處理)，而且連接資訊 (連接字串和存取認證) 是服務組態的一部分。  
  
 當啟動 Oracle CDC 服務時，它會嘗試連接到相關聯的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體、取得需要處理的 Oracle CDC 執行個體清單，然後執行初始環境驗證。 服務啟動期間的錯誤和任何啟動/停止資訊一定會寫入 Windows 應用程式事件記錄檔。 當建立與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連接時，所有錯誤和資訊訊息都會寫入 **執行個體之 MSXDBCDC 資料庫的** dbo.xdbcdc_trace [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。 啟動期間所做的其中一項檢查就是確認目前沒有同名的其他 Oracle CDC 服務正在執行。 如果目前正從另一部電腦連接同名的服務，則 Oracle CDC 服務會進入等待迴圈、等候其他服務中斷連接，然後再繼續處理 Oracle CDC 工作。  
  
 當 Oracle CDC 服務通過所有啟動驗證之後，它會檢查 MSXDBCDC 資料庫中的 **dbo.xdbcdc_databases** 資料表，看看是否有任何啟用的 Oracle CDC 執行個體。 對於每個啟用的 Oracle CDC 執行個體而言，此服務會啟動子處理序來處理該 Oracle CDC 執行個體。  
  
 當 Oracle CDC 執行個體啟動時，它會存取與 CDC 執行個體同名的 SQL Server CDC 資料庫，並從上一次執行擷取其狀態。 它也會確認所有項目是否正常執行。 然後它會繼續處理變更，讀取 Oracle 交易記錄，並將變更寫入 CDC 資料庫。  
  
 Oracle CDC 服務會定期監視 MSXDBCDC 資料庫中的 **dbo.xdbcdc_tables** 資料表，以判斷任何 Oracle CDC 執行個體組態是否有任何組態變更。 如果找到變更，Oracle CDC 服務會通知 Oracle CDC 執行個體，告知它應該檢查其組態中的變更。 當啟用 Oracle CDC 執行個體時，可以套用大多數的組態變更 (例如加入和移除擷取執行個體)，其他變更則需要重新啟動 Oracle CDC 執行個體。  
  
 當使用 Oracle CDC 設計工具主控台時，將會自動偵測變更。 當直接使用 SQL 更新 Oracle CDC 組態時，應該針對 Oracle CDC 服務呼叫以下程序來通知組態變更：  
  
```sql
DECLARE @dbname nvarchar(128) = 'HRcdc'  
EXECUTE [MSXDBCDC].[dbo].[xdbcdc_update_config_version] @dbname  
GO  
  
```  
  
 Oracle CDC 執行個體處理序會在 **cdc.xdbcdc_state** 系統資料表中更新其狀態，並將錯誤資訊寫入 **cdc.xdbcdc_trace** 資料表。 **xdbcdc_state** 資料表對於監視 Oracle CDC 執行個體的狀態很實用。 它會提供最新狀態、各種計數器 (例如從 Oracle 讀取的變更數目、寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的變更數目、寫入的認可交易數目以及目前進行中的交易數目) 和延遲指示。  
  
 Oracle CDC 執行個體組態會儲存在 **cdc.xdbcdc_config** 資料表中，這是 Oracle CDC 設計工具主控台所使用的資料表。 因為目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和 CDC 資料庫中會找到 Oracle CDC 執行個體的完整組態，所以為 Oracle CDC 執行個體建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 部署指令碼是可行的。 這會使用 Oracle CDC 服務組態和 Oracle CDC 設計工具主控台來完成。  
  
## <a name="security-considerations"></a>安全性考量  
 以下描述使用 Oracle CDC 服務所需的安全性需求。  
  
### <a name="protection-of-source-oracle-data"></a>保護來源 Oracle 資料  
 Oracle CDC 服務不需要存取 Oracle 來源資料，而且會藉由確定記錄採礦認證未提供客戶 Oracle 資料表的 SELECT 權限來保障其安全性。  
  
### <a name="protection-of-source-oracle-change-data"></a>保護來源 Oracle 變更資料  
 Oracle CDC 服務有提供記錄採礦認證，可讓服務擷取針對 Oracle 資料庫中的任何資料表所做的變更。 變更資料並不像一般資料表一樣擁有精細的存取權限，因此存取變更資料會略過內建 Oracle 資料存取控制。  
  
 擷取的來源 Oracle 資料表在 CDC 資料庫中擁有相同結構描述和資料表名稱的空白鏡像資料表。 擷取的資料會儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 擷取執行個體中，而且所提供的保護與擷取自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的變更相同。 若要存取與擷取執行個體相關聯的變更資料，使用者必須被授與相關聯鏡像資料表之所有擷取資料行的選取存取權。 此外，如果建立擷取執行個體時指定了控制角色，呼叫端也必須是指定之控制角色的成員。 雖然傳回之中繼資料的存取權通常也會使用基礎來源資料表的選取存取權以及任何已定義之控制角色的成員資格來控制，但是所有資料庫使用者都可以透過 public 角色存取用以存取中繼資料的其他一般異動資料擷取函數。  
  
 這表示，具有 **sysadmin** 固定伺服器角色或 **db_owner** 固定資料庫角色的使用者預設會擁有擷取之資料的完整存取權，而且可以透過控制角色或是授與擷取之資料行的選取存取權來進一步授與存取權。  
  
### <a name="protection-of-source-oracle-log-mining-credentials"></a>保護來源 Oracle 記錄採礦認證  
 儲存在 CDC 資料庫中的 Oracle CDC 服務組態 (在 cdc.xdbcdc_config 資料表中) 包括記錄採礦使用者名稱和其關聯的密碼。  
  
 記錄採礦密碼會透過具有固定名稱 `xdbcdc_asym_key` 的非對稱金鑰來以加密格式儲存，該金鑰會利用下列命令自動建立：  
  
```sql
USE [<cdc-database-name>]  
CREATE ASYMMETRIC KEY xdbcdc_asym_key  
    WITH ALGORITHM = RSA_1024  
    ENCRYPTION BY PASSWORD = '<cdc-database-name><asym-key-password>'  
  
```  
  
 如果使用不同的演算法，可以卸除這個金鑰以及建立由相同密碼所加密而且同名的新金鑰。  
  
 非對稱金鑰密碼是儲存在登錄中 **HKLM\Software\Microsoft\XDBCDCSVC\\<service-name>** 路徑底下的主密碼。 這個金鑰只能供本機管理員和 Oracle CDC Windows 服務帳戶存取。 此金鑰包含加密的二進位值 **AsymmetricKeyPassword** ，這個值儲存非對稱金鑰密碼。 必須擁有這個登錄機碼的存取權，才能存取 Oracle 記錄採礦認證。  
  
 若要使用 ENCRYPTION BY PASSWORD 子句，此密碼必須符合執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之電腦的 Windows 密碼原則需求。 若要進行這項處理，請根據該原則來選取非對稱金鑰密碼。  
  
 如果遺失非對稱金鑰密碼，則必須在 Oracle CDC 服務設計工具中再次指定每一個 Oracle CDC 執行個體的記錄採礦認證。  
  
 當 CDC 服務偵測到沒有此非對稱金鑰的 Oracle 執行個體 CDC 資料庫，或是金鑰存在但是密碼不相符時，就會在 CDC 資料庫中自動建立非對稱金鑰。  
  
### <a name="oracle-cdc-service-windows-service-account"></a>Oracle CDC 服務 Windows 服務帳戶  
 搭配 Oracle CDC Windows 服務使用的服務帳戶不需要任何其他權限。 這個帳戶必須能夠使用 Oracle Native Client API 和 SQL Server Native Client ODBC API。 它也必須能夠存取登錄中的服務組態機碼 (這個 CDC 服務組態主控台會設定此機碼的 ACL)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [高可用性支援](../../integration-services/change-data-capture/high-availability-support.md)  
  
-   [SQL Server 連接所需的 CDC 服務權限](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
-   [使用者角色](../../integration-services/change-data-capture/user-roles.md)  
  
-   [使用 Oracle CDC 服務](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md)  
  
## <a name="see-also"></a>另請參閱  
 [如何管理本機 CDC 服務](../../integration-services/change-data-capture/how-to-manage-a-local-cdc-service.md)   
 [管理 Oracle CDC 服務](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md)  
  
  

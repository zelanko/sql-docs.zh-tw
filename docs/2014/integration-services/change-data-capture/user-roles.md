---
title: Attunity 適用於 Oracle 的異動資料擷取服務的使用者角色 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: be0ec384-e03b-4483-96ca-02b289804d6a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 87b05f4d6d20144614954cec1b5671321e7569bb
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85435185"
---
# <a name="user-roles-for-change-data-capture-service-for-oracle-by-attunity"></a>Attunity Oracle Change Data Capture 服務的使用者角色
  本節描述 Attunity Oracle Change Data Capture (CDC) 服務的使用者角色。 描述的角色包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫角色、Windows 角色或 Oracle 資料庫角色。  
  
## <a name="windows-user-roles"></a>Windows 使用者角色  
 以下描述 Oracle CDC 服務使用的 Windows 使用者角色。  
  
### <a name="computer-administrator-oracle-cdc-service"></a>電腦管理員：Oracle CDC 服務  
 電腦管理員是負責建立和維護電腦上 CDC 服務的 Windows 使用者。 這個使用者必須屬於本機電腦管理員的群組。  
  
 Oracle CDC 服務電腦管理員所執行的工作包括：  
  
-   安裝 Oracle CDC 服務軟體  
  
-   建立 Oracle CDC Windows 服務  
  
-   設定與目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的 CDC 服務連接 (連接字串和認證)  
  
-   確定 Oracle 記錄採礦認證可透過 CDC 服務主要密碼來保障安全  
  
-   刪除 CDC 服務 Windows 服務  
  
-   解除安裝 Oracle CDC 服務軟體  
  
-   維護 Oracle CDC 服務軟體 (例如，安裝更新)  
  
-   啟動和停止 CDC 服務 Windows 服務  
  
 當使用高可用性組態 (例如 Microsoft 容錯移轉叢集) 時，電腦管理員必須具備額外的責任和權限，例如：  
  
-   在所有叢集節點上安裝和維護 Oracle CDC 服務軟體。  
  
-   在各個叢集節點上定義 CDC 服務 Windows 服務的一般叢集服務資源。  
  
-   當做授權的電腦管理員，負責管理 Oracle CDC 服務安裝所在的電腦。 這個人會安裝 Oracle CDC 服務，並使用 CDC 服務組態主控台在本機電腦上設定 Oracle CDC 服務。  
  
### <a name="service-account-oracle-cdc-service"></a>服務帳戶：Oracle CDC 服務  
 這個 Oracle CDC 服務 Windows 服務帳戶是用於執行 Oracle CDC 服務的 Windows 帳戶 (服務帳戶)。  
  
 此服務帳戶的唯一必要權限是要能夠使用 Oracle 用戶端和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 提供者。 除非特定提供者需要，否則這個帳戶不需要存取檔案 (例如，如果 Oracle 用戶端連接字串參考 **tnsnames.ora** 檔案中的 Oracle 資料庫執行個體，則該檔案必須可供服務帳戶讀取)。  
  
 當您在 Windows Vista 或 Windows Server 2008 上建立 Oracle CDC 服務時，預設服務帳戶為 NETWORK SERVICE 帳戶。  
  
 在 Windows 7、Windows Server 2008 R2 及更新版本上，預設服務帳戶為 NT Service\\<服務名稱>。  
  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在另一部電腦上執行或者為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 叢集執行個體，而且此服務需要使用 Windows 驗證連接到目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，此服務帳戶應該是網域帳戶。  
  
## <a name="sql-server-user-roles"></a>SQL Server 使用者角色  
 以下描述 Oracle CDC 服務使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者角色。  
  
### <a name="oracle-cdc-service-administrator"></a>Oracle CDC 服務管理員  
 CDC 服務管理員是可完全控制目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上之 Oracle CDC 服務成品的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者。 CDC 服務管理員會使用 Oracle CDC 設計工具主控台來設計 Oracle CDC 執行個體。  
  
 CDC 服務管理員應該被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定伺服器角色 **public** 和 **dbcreator**。  
  
 CDC 服務管理員所執行的工作包括：  
  
-   準備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來主控 Oracle CDC 執行個體 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫)。 在此工作中，將會於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中建立稱為 MSXDBCDC 的特殊資料庫。  
  
-   建立 Oracle CDC 執行個體 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 工作包括針對 CDC 啟用新建立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，這需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員 (**sysadmin**)。  
  
-   設計 Oracle CDC 執行個體。 此工作包括提供有關來源 Oracle 資料庫和擷取資料表的資訊，這需要 Oracle 資料庫管理員。  
  
-   維護一段時間的 Oracle CDC 執行個體，其中包括加入/移除擷取執行個體和更新組態。  
  
-   啟用或停用 Oracle CDC 執行個體。  
  
-   監視 Oracle CDC 執行個體的狀態。  
  
-   針對影響 Oracle CDC 執行個體的問題進行疑難排解。  
  
 CDC 服務管理員至少一開始會在與 Oracle CDC 執行個體相關聯之 **CDC 資料庫的** db_owner [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定資料庫角色中。 這會提供 CDC 服務管理員對於 CDC 資料庫中儲存之變更資料的存取權。 一旦建立，CDC 資料庫的 **db_owner** 角色就可以指派給不同的使用者，該使用者可以執行上面列出的所有工作，除了準備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和建立另一個 Oracle CDC 執行個體以外。  
  
 CDC 服務管理員不需要知道建立 Oracle CDC Windows 服務所指定的主要密碼。  
  
### <a name="system-administrator"></a>系統管理員  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者，而且應該將與 Oracle CDC 服務相關聯之 **執行個體的** 系統管理員 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定伺服器角色授與給他。  
  
 只有一個 Oracle CDC 特有的工作需要由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員執行，也就是針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 的 Oracle CDC 執行個體啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 在建立新的 Oracle CDC 執行個體時，便會使用 Oracle CDC 設計工具主控台執行此工作。  
  
### <a name="oracle-cdc-service-user"></a>Oracle CDC 服務使用者  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 服務使用者是由 Oracle CDC 服務所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，可針對 MSXDBCDC 以及此服務所處理的所有 Oracle CDC 執行個體 (CDC 資料庫) 來執行其工作。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 服務使用者應該被授與以下權限：  
  
-   伺服器所處理之所有 CDC 資料庫的固定資料庫角色 **db_dlladmin**、 **db_datareader**和 **db_datawriter** 的成員。  
  
-   MSXDBCDC 資料庫之固定資料庫角色 **db_datareader** 和 **db_datawriter** 的成員。  
  
 因為 Oracle CDC 服務會使用單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入處理所有 CDC 資料庫和 MSXDBCDC 資料庫，所以應該在所有的這些資料庫中對應這個登入。  
  
### <a name="oracle-cdc-change-consumer"></a>Oracle CDC 變更取用者  
 Oracle CDC 變更取用者是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者，他會取用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 執行個體資料庫中 CDC 資料表內所儲存的變更。  
  
 這個使用者會決定透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 基礎結構所產生的 CDC 功能來存取每一個 CDC 資料表所需的使用者角色。 如果在指定擷取執行個體時並未指定任何使用者角色，則變更的存取只限於 CDC 資料庫的 **db_owner** 固定資料庫角色成員。  
  
## <a name="oracle-user-roles"></a>Oracle 使用者角色  
 以下描述 Oracle CDC 服務使用的 Oracle 使用者角色。  
  
### <a name="database-administrator-dba"></a>資料庫管理員 (DBA)  
 Oracle 資料庫管理員 (DBA) 是 Oracle 資料庫使用者。 Oracle DBA 所執行的工作包括：  
  
-   設定來源 Oracle 資料庫在 ARCHIVELOG 模式工作。  
  
-   設定擁有必要權限的記錄採礦使用者。  
  
-   為擷取的資料表設定補充記錄。  
  
-   幫助還原不再可用的封存交易記錄檔，以便進行處理。  
  
 Oracle 資料庫管理員可以取得需要執行的 Oracle SQL 指令碼，以便可以在執行之前加以評估。 Oracle 資料庫管理員還可以直接從 Oracle CDC 設計工具主控台執行 Oracle SQL 指令碼。  
  
 如果 Oracle 資料庫管理員選擇使用 Oracle CDC 設計工具主控台，則不會保存管理員的認證，除了使用這些認證的內容 (對話) 以外。  
  
 Oracle 資料庫管理員會與 Oracle CDC 服務管理員一起協調 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 執行個體組態的工作。  
  
### <a name="log-mining-user"></a>記錄採礦使用者  
 Oracle 記錄採礦器使用者是特殊的 Oracle 資料庫使用者，他會被授與存取和處理 Oracle 交易記錄的必要權限。  
  
 這個使用者的認證會使用非對稱金鑰加密儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 執行個體資料庫中。 這些認證僅供 Oracle CDC 服務存取，而無法供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 執行個體資料庫擁有者存取。  
  
 下列清單描述記錄採礦使用者應該被授與的必要權限：  
  
-   選取 [開啟]\<any-captured-table>  
  
-   SELECT ANY TRANSACTION  
  
-   EXECUTE on DBMS_LOGMNR  
  
-   SELECT on V$LOGMNR_CONTENTS  
  
-   SELECT on V$ARCHIVED_LOG  
  
-   SELECT on V$LOG  
  
-   SELECT on V$LOGFILE  
  
-   SELECT on V$DATABASE  
  
-   SELECT on V$THREAD  
  
-   SELECT on V$PARAMETER  
  
-   SELECT on DBA_REGISTRY  
  
-   SELECT on ALL_INDEXES  
  
-   SELECT on ALL_OBJECTS  
  
-   SELECT on DBA_OBJECTS  
  
-   SELECT on ALL_TABLES  
  
 如果有任何權限不能授與給 V$xxx，則應該授與給 V $xxx。  
  
### <a name="schema-user"></a>結構描述使用者  
 Oracle 結構描述使用者是具有要擷取之 Oracle 資料表結構描述讀取存取權的 Oracle 使用者。 當使用 Oracle CDC 設計工具主控台來擷取 Oracle 結構描述、要擷取的資料表以及其資料行、索引和索引鍵的清單時，便需要這個使用者。  
  
 絕對不會儲存這個使用者的認證。 每當需要這些認證時，CDC 設計工具主控台便會要求這些認證，而且在其餘 UI 工作階段會保存這些認證。  
  
  

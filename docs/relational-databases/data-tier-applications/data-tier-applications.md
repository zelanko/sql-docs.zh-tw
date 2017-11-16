---
title: "資料層應用程式 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 08/12/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- designing DACs
- How to [DAC]
- data-tier application [SQL Server], designing
- wizard [DAC]
ms.assetid: a04a2aba-d07a-4423-ab8a-0a31658f6317
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ab8a8fded3daac09e9d7b90ba3a734a46fd4cce0
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="data-tier-applications"></a>資料層應用程式
  資料層應用程式 (DAC) 是邏輯資料庫管理實體，會定義與使用者資料庫相關聯的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件，如資料表、檢視表，以及包括登入的執行個體物件。 DAC 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫部署的自主單位，可讓資料層開發人員和資料庫管理員將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件包裝為可攜式成品，稱為 DAC 封裝，又稱為 DACPAC。  
  
 BACPAC 是相關的成品，會封裝資料庫結構描述，以及在資料庫中儲存的資料。  
  
## <a name="benefits-of-data-tier-applications"></a>資料層應用程式的優點  
 大多數資料庫應用程式的開發週期包含開發人員和 DBA 共用及交換應用程式更新和維護活動的指令碼和特定整合注意事項。 雖然這對小量資料庫是可接受的，但是一旦資料庫數目、大小和複雜性等方面都增加時，這很快會變得無法擴充。  
  
 DAC 是資料庫生命週期管理和生產力工具，讓宣告式資料庫開發可以簡化部署和管理。 開發人員可以在 SQL Server Data Tools 資料庫專案中撰寫資料庫，然後建立資料庫成為 DACPAC 以遞交給 DBA。 DBA 可以使用 SQL Server Management Studio，將 DAC 部署至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 測試或實際執行的執行個體或 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。 或者，DBA 可以使用 DACPAC 來升級以前使用 SQL Server Management Studio 部署的資料庫。 為了完成開發週期，DBA 可以將資料庫擷取至 DACPAC 並將它遞交給開發人員，以反映測試或實際執行調整，或啟用進一步的資料庫設計變更以回應應用程式變更。  
  
 DAC 驅動部署優於指令碼驅動方法，因為此工具協助 DBA 識別及驗證不同來源和目標資料庫的行為。 在升級期間，如果升級可能會導致資料遺失，工具會警告 DBA，而且還提供升級計畫。 DBA 可以評估該計畫，然後利用該工具進行升級。  
  
 DAC 還支援版本設定，協助開發人員和 DBA 維護和管理資料庫生命週期中的資料庫歷程。  
  
## <a name="dac-concepts"></a>DAC 概念  
 DAC 會簡化支援應用程式之資料層元素的開發、部署與管理：  
  
-   資料層應用程式 (DAC) 是邏輯資料庫管理實體，會定義與使用者資料庫相關聯的所有 SQL Server 物件，例如資料表、檢視表和執行個體物件。 它是 SQL Server 資料庫部署的自主單位，可讓資料層開發人員和 DBA 將 SQL Server 物件包裝為可攜式成品，稱為 DAC 封裝或 .dacpac 檔案。  
  
-   SQL Server 資料庫若要被視為 DAC，必須註冊，無論是透過使用者作業明確註冊，或其中一個 DAC 作業隱含註冊。 當資料庫註冊時，就會記錄 DAC 版本和其他屬性做為資料庫中繼資料的一部分。 相反地，資料庫也可以取消註冊並移除其 DAC 屬性。  
  
-   DAC 工具通常能夠讀取舊版 SQL Server DAC 工具所產生的 DACPAC 檔案，也可以將 DACPAC 部署至舊版 SQL Server。 不過，舊版 DAC 工具無法讀取新版 DAC 工具所產生的 DACPAC 檔案。 具體來說：  
  
    -   DAC 作業是在 SQL Server 2008 R2 中導入。 除了 SQL Server 2008 R2 資料庫之外，工具還支援 SQL Server 2008、SQL Server 2005 和 SQL Server 2000 資料庫所產生的 DACPAC 檔案。  
  
    -   除了 SQL 2016 資料庫之外，SQL Server 2016 隨附的工具還可以讀取 SQL Server 2008 R2 或 SQL Server 2012 隨附的 DAC 工具所產生的 DACPAC 檔案。 這包含 SQL Server 2014、2012、2008 R2、2008 和 2005 資料庫，但**不包含** SQL Server 2000 資料庫。  
  
    -   SQL Server 2008 R2 的 DAC 工具無法讀取 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 工具所產生的 DACPAC 檔案。  
  
-   DACPAC 是副檔名為 .dacpac 的 Windows 檔案。 檔案支援開放式格式，包含代表 DACPAC 來源詳細資料、資料庫的物件和其他特性的多個 XML 區段。 進階使用者可以使用產品隨附的 DacUnpack.exe 公用程式來解除封裝檔案，更仔細檢查每個區段。  
  
-   使用者必須是 dbmanager 角色的成員或被指派 CREATE DATABASE 權限，才能建立資料庫，包括部署 DAC 封裝來建立資料庫。 使用者必須是 dbmanager 角色的成員或被指派 DROP DATABASE 權限，才能卸除資料庫。  
  
## <a name="dac-tools"></a>DAC 工具  
 DACPAC 可以橫跨 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 隨附的多個工具緊密地使用。 這些工具將 DACPAC 做為互通性單位，解決不同使用者角色的需求。  
  
-   應用程式開發人員：  
  
    -   可以使用 SQL Server Data Tools 資料庫專案來設計資料庫。 此專案成功建立會導致產生包含在 .dacpac 檔案中的 DACPAC。  
  
    -   可以將 DACPAC 匯入資料庫專案中並繼續進行資料庫設計。  
  
        SQL Server Data Tools 還支援 Local DB，以進行未連接的用戶端資料庫應用程式開發。 開發人員可以取得此本機資料庫的快照集，以建立包含在 .dacpac 檔案中的 DACPAC。  
  
    -   開發人員可以獨立地將資料庫專案直接發行至資料庫，甚至不需產生 DACPAC。 發行作業遵循類似於其他工具部署作業的行為。  
  
-   資料庫管理員：  
  
    -   可以使用 SQL Server Management Studio 從現有的資料庫中擷取 DACPAC，也可以執行其他 DAC 作業。  
  
    -   此外，[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的 DBA 可以使用 SQL Azure 管理入口網站執行 DAC 作業。  
  
-   獨立軟體廠商：  
  
    -   SQL Server 主機服務和其他資料管理產品可以使用 DACFx API 執行 DAC 作業。  
  
-   IT 系統管理員：  
  
    -   IT 系統整合人員和管理員可以使用 SqlPackage.exe 命令列工具執行 DAC 作業。  
  
## <a name="dac-operations"></a>DAC 作業  
 DAC 支援下列作業：  
  
-   **EXTRACT** – 使用者可將資料庫擷取到 DACPAC。  
  
-   **DEPLOY** – 使用者可將 DACPAC 部署到主機伺服器。 從管理功能工具 (如 SQL Server Management Studio 或 SQL Azure 管理入口網站) 完成部署後，主機伺服器上所產生的資料庫會隱含註冊為資料層應用程式。  
  
-   **REGISTER** – 使用者可將資料庫註冊為資料層應用程式。  
  
-   **UNREGISTER** – 以前註冊為 DAC 的資料庫可以取消註冊。  
  
-   **UPGRADE** – 可以使用 DACPAC 來升級資料庫。 即使以前未註冊為資料層應用程式的資料庫也支援升級，但因為升級，資料庫會隱含註冊。  
  
## <a name="bacpac"></a>BACPAC  
 BACPAC 是副檔名為 .bacpac 的 Windows 檔案，可封裝資料庫的結構描述和資料。 BACPAC 的主要使用案例是將資料庫從某個伺服器移至另一個伺服器 (或[將資料庫從本機伺服器移轉至雲端](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/))，以及以開放式格式封存現有資料庫。  
  
 類似於 DACPAC，BACPAC 檔案格式是開放式；BACPAC 的結構描述內容與 DACPAC 的結構描述內容相同。 BACPAC 中的資料是以 JSON 格式儲存。  
  
 DACPAC 和 BACPAC 相似，但它們以不同的案例為目標。 DACPAC 專注於擷取及部署架結構描述，包括升級現有資料庫。 DACPAC 的主要使用案例是將嚴格定義的結構描述部署至開發、測試，最後至實際執行環境。 也以及反向：擷取實際執行的結構描述並將它反向套用至測試和開發環境。  
  
 另一方面，BACPAC 專注於擷取支援兩個主要作業的結構描述和資料：  
  
-   **EXPORT**– 使用者可將資料庫的結構描述和資料匯出至 BACPAC。  
  
-   **IMPORT** – 使用者可以將結構描述和資料匯入主機伺服器中的新資料庫。  
  
 下列資料庫管理工具支援這兩個功能：SQL Server Management Studio、Azure 入口網站和 DACFx API。  
  
## <a name="permissions"></a>Permissions  
 您必須是 **dbmanager** 角色的成員或被指派 **CREATE DATABASE** 權限，才能建立資料庫，包括部署 DAC 封裝來建立資料庫。 您必須是 **dbmanager** 角色的成員或被指派 **DROP DATABASE** 權限，才能卸除資料庫。  
  
## <a name="data-tier-application-tasks"></a>資料層應用程式工作  
  
|工作|主題連結|  
|----------------------|-----------|  
|描述如何使用 DAC 封裝檔案來建立新的 DAC 執行個體。|[部署資料層應用程式](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)|  
|描述如何使用新的 DAC 封裝檔案，將執行個體升級為新版的 DAC。|[升級資料層應用程式](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)|  
|描述如何移除 DAC 執行個體。 您可以選擇同時卸離或卸除相關聯的資料庫，或讓資料庫保持完整。|[刪除資料層應用程式](../../relational-databases/data-tier-applications/delete-a-data-tier-application.md)|  
|描述如何使用 SQL Server 公用程式來檢視目前已部署 DAC 的健全狀態。|[監視資料層應用程式](../../relational-databases/data-tier-applications/monitor-data-tier-applications.md)|  
|描述如何建立包含在 DAC 中的資料和中繼資料之封存的 .bacpac 檔案。|[匯出資料層應用程式](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)|  
|描述如何使用 DAC 封存檔案 (.bacpac) 執行 DAC 的邏輯還原，或將 DAC 移轉至另一個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 或 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的執行個體。|[匯入 BACPAC 檔案以建立新的使用者資料庫](../../relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)|  
|描述如何匯入 BACPAC 檔案，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體內建立新的使用者資料庫。|[從資料庫中擷取 DAC](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)|  
|描述如何將現有的資料庫升級為 DAC 執行個體。 DAC 定義會建立並儲存在系統資料庫中。|[將資料庫註冊為 DAC](../../relational-databases/data-tier-applications/register-a-database-as-a-dac.md)|  
|描述如何先檢閱 DAC 封裝的內容以及 DAC 升級要執行的動作，再於實際執行系統中使用該封裝。|[驗證 DAC 套件](../../relational-databases/data-tier-applications/validate-a-dac-package.md)|  
|描述如何先將 DAC 封裝的內容放入資料庫管理員可以檢閱 DAC 作用的資料夾，再將它部署至實際伺服器。|[解除封裝 DAC 套件](../../relational-databases/data-tier-applications/unpack-a-dac-package.md)|  
|描述如何使用精靈來部署現有的資料庫。 精靈會使用 DAC 來執行這種部署。|[使用 DAC 部署資料庫](../../relational-databases/data-tier-applications/deploy-a-database-by-using-a-dac.md)|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 物件與版本的 DAC 支援](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)  
  
  

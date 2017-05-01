---
title: "SQL Server 物件與版本的 DAC 支援 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data-tier application [SQL Server], supported objects
- objects [SQL Server], data-tier applications
ms.assetid: b1b78ded-16c0-4d69-8657-ec57925e68fd
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6c6fa912592feefe48ce023f58fbf032d64004e6
ms.lasthandoff: 04/11/2017

---
# <a name="dac-support-for-sql-server-objects-and-versions"></a>SQL Server 物件與版本的 DAC 支援
  資料層應用程式 (DAC) 支援最常用的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 物件。  
  
 **本主題內容**  
  
-   [支援的 SQL Server 物件](#SupportedObjects)  
  
-   [SQL Server 版本的資料層應用程式支援](#SupportByVersion)  
  
-   [資料部署限制](#DeploymentLimitations)  
  
-   [部署動作的其他考量](#Considerations)  
  
##  <a name="SupportedObjects"></a> 支援的 SQL Server 物件  
 在撰寫或編輯資料層應用程式時，只能在其中指定支援的物件。 您無法從包含 DAC 不支援之物件的現有資料庫中擷取、註冊或匯入 DAC。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援下列 DAC 中的物件。  
  
|||  
|-|-|  
|DATABASE ROLE|FUNCTION：內嵌資料表值|  
|FUNCTION：多重陳述式資料表值|FUNCTION：純量|  
|INDEX：叢集|INDEX：非叢集|  
|INDEX：空間|INDEX：唯一|  
|LOGIN|Permissions|  
|角色成員資格|SCHEMA|  
|Statistics|STORED PROCEDURE：Transact-SQL|  
|同義字|TABLE：檢查條件約束|  
|TABLE：定序|TABLE：資料行，包括計算資料行|  
|TABLE：條件約束，預設值|TABLE：條件約束，外部索引鍵|  
|TABLE：條件約束，索引|TABLE：條件約束，主索引鍵|  
|TABLE：條件約束，唯一|TRIGGER：DML|  
|TYPE：HIERARCHYID、GEOMETRY、GEOGRAPHY|TYPE：使用者定義資料類型|  
|TYPE：使用者定義資料表類型|USER|  
|VIEW||  
  
##  <a name="SupportByVersion"></a> SQL Server 版本的資料層應用程式支援  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各版本對 DAC 作業有不同的支援層級。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的所有 DAC 作業，受到該版本的所有版本支援 (例如 Standard、Enterprise、Developer 或 Evaluation)。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體支援下列 DAC 作業：  
  
-   所有支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本都支援匯出和擷取。  
  
-   [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 以及所有 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]版本都支援所有作業。  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Service Pack 2 (SP2) 或更新版本以及 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 或更新版本都支援所有作業。  
  
 DAC Framework 包含用戶端工具，以建立和處理 DAC 封裝和匯出檔案。 下列產品包含 DAC Framework  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 包含可支援所有 DAC 作業的 DAC Framework 3.0。  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 和 Visual Studio 2010 SP1 包含 DAC Framework 1.1，它可支援不含匯出和匯入的所有 DAC 作業。  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 和 Visual Studio 2010 包含可支援不含匯出、匯入和就地升級之所有 DAC 作業的 DAC Framework 1.0。  
  
-   舊版 SQL Server 或 Visual Studio 的用戶端工具不支援 DAC 作業。  
  
 舊版 DAC Framework 無法處理使用其中一個 DAC Framework 版本所建立的 DAC 封裝或匯出檔案。 例如，您無法使用 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 用戶端工具部署使用 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 用戶端工具所擷取的 DAC 封裝。  
  
 任何新版 DAC Framework 都可以處理使用其中一個 DAC Framework 版本所建立的 DAC 封裝或匯出檔案。 例如，您可以使用 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 或新版用戶端工具部署使用 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 用戶端工具所擷取的 DAC 封裝。  
  
##  <a name="DeploymentLimitations"></a> 資料部署限制  
 請注意在 SQL Server 2012 SP1 中 DAC Framework 資料部署引擎內的這些精確度限制。 這些限制適用於下列 DAC Framework 動作：部署或發行 .dacpac 檔案，以及匯入 .bacpac 檔案。  
  
1.  在某些情況下遺失中繼資料及 sql_variant 資料行內的基底類型。 在受影響的案例下，您將會看見包含下列訊息的警告：  **當由 DAC Framework 部署時，不會保存 sql_variant 資料行內使用之某些資料類型的某些屬性。**  
  
    -   MONEY、SMALLMONEY、NUMERIC、DECIMAL 基底類型：不會保存有效位數。  
  
        -   DECIMAL/NUMERIC 基底類型的有效位數為 38：“TotalBytes” sql_variant 中繼資料一定會設定為 21。  
  
    -   所有文字基底類型：所有文字都會套用資料庫的預設定序。  
  
    -   BINARY 基底類型：不會保留最大長度屬性。  
  
    -   TIME、DATETIMEOFFSET 基底類型：有效位數一定會設定為 7。  
  
2.  在 sql_variant 資料行內遺失資料。 在受影響的案例中，您將會看見包含下列訊息的警告：**當由 DAC Framework 部署小數位數大於 3 之 sql_variant DATETIME2 資料行中的值，將會遺失資料。DATETIME2 值在部署期間限制為小數位數等於 3。**  
  
    -   小數位數大於 3 的 DATETIME2 基底類型：小數位數限制為等於 3。  
  
3.  部署作業會因為 sql_variant 資料行內的以下情況而失敗。 在受影響的案例中，您將會看見包含下列訊息的對話方塊：  **由於 DAC Framework 中的資料限制，所以作業失敗。**  
  
    -   DATETIME2、SMALLDATETIME 和 DATE 基底類型：如果此值超出 DATETIME 範圍，例如，年份小於 1753。  
  
    -   DECIMAL、NUMERIC 基底類型：如果值的有效位數大於 28。  
  
##  <a name="Considerations"></a> 部署動作的其他考量  
 請注意，DAC Framework 資料部署動作有下列考量：  
  
-   **擷取/匯出** - 使用 DAC Framework 從資料庫建立封裝的動作 – 例如，擷取 .dacpac 檔案、匯出 .bacpac 檔案 - 這些限制都不適用。 封裝中的資料為來源資料庫中資料的不失真表示法。 如果封裝中有上述的任一情況，則擷取/匯出記錄將會透過上述的訊息包含問題摘要。 這是為了警告使用者，他們所建立的封裝中可能會發生資料部署問題。 使用者也會在記錄中看到以下摘要訊息：**這些限制不會影響 DAC Framework 所建立之 DAC 封裝中儲存之資料類型和值的精確度，而只適用於將 DAC 封裝部署到資料庫所產生的資料類型和值。如需受影響的資料以及如何解決這個限制的詳細資訊，請參閱**[這個主題](http://go.microsoft.com/fwlink/?LinkId=267086)。  
  
-   **部署/發行/匯入** - 使用 DAC Framework 將封裝部署到資料庫的動作，例如部署或發行 .dacpac 檔案以及匯入 .bacpac 檔案，這些限制都適用。 目標資料庫中產生的資料可能不包含封裝中資料的不失真表示法。 部署/匯入記錄將會在每個執行個體遇到問題時包含一則訊息 (如上所述)。 錯誤將封鎖此作業 – 請參閱上面的類別目錄 3 - 但是在其他警告的情況下將會繼續。  
  
     如需此案例中受影響的資料以及如何解決部署/發行/匯入動作之這項限制的詳細資訊，請參閱 [這個主題](http://go.microsoft.com/fwlink/?LinkId=267087)。  
  
-   **因應措施** - 擷取和匯出作業會將不失真的 BCP 資料檔寫入 .dacpac 或 .bacpac 檔案中。 為了避免限制，請使用 SQL Server BCP.exe 命令列公用程式，將不失真的資料從 DAC 封裝部署到目標資料庫。  
  
## <a name="see-also"></a>另請參閱  
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)  
  
  

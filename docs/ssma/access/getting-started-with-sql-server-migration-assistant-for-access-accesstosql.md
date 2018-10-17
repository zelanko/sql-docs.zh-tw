---
title: 開始使用 SQL Server 移轉小幫手的存取 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- error list pane
- getting started
- menus
- metadata explorers
- output pane
- toolbars
- user interface
- user interface overview
ms.assetid: 462a731f-08f1-44e1-9eeb-4deac6d2f6c5
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 1168609d35a266f2ac5fe6641aee7ca131bc9d89
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668666"
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>開始使用 SQL Server Migration Assistant for Access (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉小幫手 (SSMA) 的存取可讓您快速轉換至 Access 資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 物件上傳到產生的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，並將資料從存取移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 如果有必要，您也可以連結來存取資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 資料表，好讓您可以繼續使用現有存取前端應用程式與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。  
  
本主題介紹安裝程序，並可協助您熟悉 SSMA 使用者介面。  
  
## <a name="installing-ssma"></a>安裝 SSMA  
若要使用 SSMA，您必須先安裝 SSMA 用戶端程式可以存取您想要移轉的這兩個資料庫的電腦和目標執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 如需安裝指示，請參閱[安裝 SQL Server Migration Assistant for Access &#40;AccessToSQL&#41;](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md)。  
  
若要啟動 SSMA，請按一下**開始**，指向**所有程式**，指向**SQL Server Migration Assistant for Access**，然後選取  **SQL Server 移轉Assistant for Access**。  
  
## <a name="using-ssma"></a>使用 SSMA  
安裝之後 SSMA，最好先熟悉 SSMA 使用者介面將 Access 資料庫移轉至使用工具之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 SSMA 使用者介面，包括中繼資料瀏覽器、 中繼資料、 工具列、 輸出 窗格中，以及錯誤清單 窗格會顯示在下圖中：  
  
![SSMA for Access 圖形化使用者介面](../../ssma/access/media/ssmaforaccessgui.gif "SSMA for Access 圖形化使用者介面")  
  
若要啟動移轉，建立新的專案，然後再加入 Access 資料庫來存取中繼資料總管。 您可以再以滑鼠右鍵按一下執行工作，例如存取中繼資料總管 中的物件：
- 匯出至 Access 資料庫物件的詳細目錄[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。
- 建立報表以評估轉換為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。
- 轉換到存取結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 結構描述。

您也可以使用工具列和功能表來執行這些工作。  
  
您也必須連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 成功連線之後，階層[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫會出現在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管。 在轉換到存取結構描述之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構描述，您可以選取這些已轉換的結構描述中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管，然後載入至結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
如果您已在 新增專案 對話方塊中的下拉式清單從 移轉選取 Azure SQL DB，您必須連接到 Azure SQL DB。 成功連接之後，Azure SQL DB 資料庫的階層架構就會出現在 Azure SQL DB 中繼資料總管 中。 您將存取結構描述轉換至 Azure SQL DB 結構描述之後，您可以這些已轉換的結構描述總管中選取 Azure SQL DB 中繼資料，並接著載入至結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
載入轉換結構描述之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 中，您可以返回存取中繼資料總管 並將資料從 Access 資料庫移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 資料庫。 如果有必要，您也可以連結來存取資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 的資料表。  
  
如需有關這些工作，以及如何執行這些的詳細資訊，請參閱下列主題：  
  
-   [準備移轉的 Access 資料庫](preparing-access-databases-for-migration-accesstosql.md)  
  
-   [將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
-   [連結到 SQL Server 的 Access 應用程式](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
下列各節說明的 SSMA 使用者介面的功能。  
  
### <a name="metadata-explorers"></a>中繼資料瀏覽器  
SSMA 包含兩個中繼資料瀏覽器，您可以使用瀏覽並執行動作的存取和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 資料庫。  
  
#### <a name="access-metadata-explorer"></a>存取中繼資料總管  
存取中繼資料總管 會顯示已新增至專案的存取資料庫的詳細資訊。 當您新增 Access 資料庫時，SSMA 會擷取該資料庫，也就是可存取中繼資料總管 中的中繼資料相關的中繼資料。  
  
您可以使用存取中繼資料總管 來執行下列工作：  
  
-   瀏覽每個存取資料庫中的資料表。  
  
-   選取轉換的物件，並將轉換至物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法。 如需詳細資訊，請參閱 [ 轉換的 Access 資料庫物件](converting-access-database-objects-accesstosql.md)。  
  
-   選取的資料移轉的物件，然後將資料從這些物件移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 <<c0> [ 將 Access 資料移轉到 SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)。  
  
-   連結和取消連結存取和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 或 Azure SQL DB 中繼資料總管  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure SQL DB 中繼資料總管 會顯示執行個體的相關資訊或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 當您連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB、 SSMA 擷取該執行個體相關的中繼資料，並將它儲存在專案檔中。  
  
您可以使用 SQL Server 或 Azure SQL DB 中繼資料總管 來選取轉換的 Access 資料庫物件和載入 （同步處理） 的執行個體到這些物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。  
  
如需詳細資訊，請參閱 <<c0> [ 載入轉換的資料庫物件載入 SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)。  
  
### <a name="metadata"></a>中繼資料  
右邊的每個中繼資料總管 會描述所選的物件的索引標籤。 比方說，如果您在存取中繼資料總管 中選取資料表，四個索引標籤會出現：**表格**，**型別對應**，**屬性**，以及**資料**. 如果您選取的資料表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管 中，三個索引標籤會顯示：**表格**， **SQL**，和**資料**。  
  
大部分的中繼資料設定是唯讀的。 不過，您可以變更下列中繼資料：  
  
-   在存取中繼資料總管 中，您可能會改變型別對應。 請務必在您建立報表，或將結構描述轉換之前進行這些變更。  
  
-   在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管 中，您可以在變更資料表和索引的屬性**表格** 索引標籤。進行這些變更，再將結構描述載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 [ 轉換的 Access 資料庫物件](converting-access-database-objects-accesstosql.md)。  
  
### <a name="toolbars"></a>工具列  
SSMA 會有兩個工具列： 專案工具列和移轉工具列。  
  
#### <a name="the-project-toolbar"></a>[專案] 工具列  
[專案] 工具列包含按鈕使用專案、 加入 Access 資料庫檔案，以及連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 這些按鈕上類似的命令**檔案**功能表。  
  
#### <a name="the-migration-toolbar"></a>[移轉] 工具列  
[移轉] 工具列包含下列命令：  
  
|按鈕|函數|  
|----------|------------|  
|**轉換、載入和移轉**|將 Access 資料庫轉換、 載入轉換的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，並移轉資料至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB，全都放在一個步驟。|  
|**建立報表**|將選取的存取結構描述的轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 的語法，然後建立報表，其中顯示已成功的轉換。<br /><br />只有在存取中繼資料總管 中選取物件時，此命令才能使用。|  
|**將結構描述轉換**|將選取的存取結構描述的轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 結構描述。<br /><br />只有在存取中繼資料總管 中選取物件時，此命令才能使用。|  
|**將資料移轉**|將資料從 Access 資料庫移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。 執行此命令之前，您必須將轉換的存取結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 結構描述，然後載入到物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。<br /><br />只有在存取中繼資料總管 中選取物件時，此命令才能使用。|  
|**停止**|停止目前的處理序，例如將轉換物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 語法。|  
  
### <a name="menus"></a>功能表  
SSMA 會包含下列功能表：  
  
|功能表|描述|  
|--------|---------------|  
|**檔案**|移轉精靈，使用專案中，新增和移除存取資料庫檔案，以及連接到包含命令[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB。|  
|**編輯**|包含用來尋找和使用的詳細資料頁面中，例如複製的文字命令[!INCLUDE[tsql](../../includes/tsql-md.md)]從 [SQL 詳細資料] 窗格。 若要開啟 **管理書籤** 對話方塊的 編輯 功能表中，按一下 管理書籤。 在對話方塊中，您會看到一份現有的書籤。 您可以使用對話方塊右側的按鈕，來管理書籤。|  
|**[檢視]**|包含**同步處理中繼資料瀏覽器**命令。 這會同步處理存取中繼資料總管 之間的物件和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL DB 中繼資料總管。 也包含命令，以顯示或隱藏**輸出**並**錯誤清單**窗格和選項**版面配置**來管理與配置。|  
|**工具**|包含命令來建立報表、 匯出資料、 將物件和資料移轉、 連結的資料表，並提供存取全域和專案設定對話方塊。|  
|**說明**|提供存取至 SSMA 協助和**關於** 對話方塊。|  
  
### <a name="output-pane-and-error-list-pane"></a>輸出窗格和 [錯誤清單] 窗格  
**檢視** 功能表提供切換可見性的 輸出 窗格和 錯誤清單 窗格的命令：  
  
-   [輸出] 窗格會顯示在物件轉換、 物件同步處理和資料移轉期間從 SSMA 的狀態訊息。  
  
-   [錯誤清單] 窗格會顯示錯誤、 警告和參考用訊息的清單中，您可以排序。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  

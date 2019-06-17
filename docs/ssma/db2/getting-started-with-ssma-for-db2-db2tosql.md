---
title: 開始使用 SSMA for DB2 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 86a931c9132a23d9ceb3d46b48fbdce23bf76f92
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298859"
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>開始使用 SSMA for DB2 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉小幫手 (SSMA) for DB2 可讓您快速轉換至 DB2 資料庫結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構描述上傳到產生的結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並將資料從 DB2，以便移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
本主題介紹安裝程序，並接著可幫助您熟悉 SSMA 使用者介面。  
  
## <a name="installing-ssma"></a>安裝 SSMA  
若要使用 SSMA，您必須先安裝 SSMA 用戶端程式可以存取來源 DB2 資料庫和目標執行個體的電腦上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 正在執行的電腦上的 DB2 OLEDB 提供者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這些元件支援的資料移轉和 DB2 系統函數的模擬。 如需安裝指示，請參閱[安裝 SSMA for DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)。  
  
若要啟動 SSMA，請按一下**開始**，指向**所有程式**，指向 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for DB2**，然後按一下 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB2 的移轉小幫手**。  
  
## <a name="ssma-for-db2-user-interface"></a>SSMA for DB2 的使用者介面  
安裝 SSMA 之後，您可以將 DB2 資料庫移轉至使用 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 最好先熟悉 SSMA 使用者介面在開始之前。 下圖顯示的 SSMA，包括中繼資料瀏覽器、 中繼資料、 工具列、 輸出 窗格中，以及錯誤清單 窗格中的使用者介面：  
  
![SSMA 使用者介面](../../ssma/db2/media/ssma_db2_ui.png "SSMA 使用者介面")  
  
若要啟動移轉，您必須先建立新的專案。 然後，您會連接至 DB2 資料庫。 成功連線之後，DB2 結構描述會出現在 DB2 中繼資料總管。 接著以滑鼠右鍵按一下物件，在 DB2 中繼資料總管 來執行工作，例如建立評估轉換的報表，您可以[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您也可以使用工具列和功能表來執行這些工作。  
  
您也必須連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 成功連線之後，階層[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫會出現在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管。 轉換 DB2 結構描述之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構描述中，選取這些已轉換的結構描述中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管，然後再同步處理與結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
同步處理已轉換的結構描述後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您可以返回 [DB2 中繼資料總管]，然後將資料從 DB2 結構描述移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。  
  
如需有關這些工作，以及如何執行這些的詳細資訊，請參閱[將 DB2 資料庫移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)。  
  
下列各節說明的 SSMA 使用者介面的功能。  
  
### <a name="metadata-explorers"></a>中繼資料瀏覽器  
SSMA 包含兩個中繼資料瀏覽器，瀏覽，並在 DB2 上執行動作和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。  
  
#### <a name="db2-metadata-explorer"></a>DB2 Metadata Explorer  
DB2 中繼資料總管 會顯示 DB2 結構描述的相關資訊。 藉由使用 DB2 中繼資料總管，您可以執行下列工作：  
  
-   瀏覽每個結構描述中的物件。  
  
-   選取轉換的物件，然後將轉換至物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法。 如需詳細資訊，請參閱 <<c0> [ 轉換 DB2 結構描述&#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)。</c0>  
  
-   選取資料表資料移轉，然後從這些資料表，以進行移轉資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需詳細資訊，請參閱 <<c0> [ 將 DB2 資料庫移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)。</c0>  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server Metadata Explorer  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中繼資料總管 會顯示相關的執行個體資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 當您連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，SSMA 擷取該執行個體相關的中繼資料，並將它儲存在專案檔中。  
  
您可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管，選取已轉換的 DB2 資料庫物件，並與執行個體，然後同步處理這些物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
### <a name="metadata"></a>中繼資料  
右邊的每個中繼資料總管 會描述所選的物件的索引標籤。 例如，如果您在 DB2 中繼資料總管 中選取資料表，就會出現六個索引標籤：**表格**， **SQL**，**輸入對應時，報表**，**屬性**，並**資料**。 **報表** 索引標籤包含的資訊，建立報表之後，就會包含選取的物件。 如果您選取的資料表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管 中，三個索引標籤會出現：**表格**， **SQL**，以及**資料**。  
  
大部分的中繼資料設定是唯讀的。 不過，您可以變更下列中繼資料：  
  
-   在 DB2 中繼資料總管 中，您可以改變程序，及類型對應。 若要轉換的變更的程序和類型對應，進行變更，將結構描述的轉換之前。  
  
-   在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管] 中，您可以改變[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序。 若要查看這些變更的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，載入將結構描述之前，進行這些變更[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
在 [中繼資料總管] 中所做的變更會反映專案中繼資料，不在來源或目標資料庫中。  
  
### <a name="toolbars"></a>工具列  
SSMA 會有兩個工具列： 專案工具列和移轉工具列。  
  
#### <a name="the-project-toolbar"></a>[專案] 工具列  
[專案] 工具列包含按鈕使用專案、 連接至 DB2，以及連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這些按鈕上類似的命令**檔案**功能表。  
  
#### <a name="migration-toolbar"></a>移轉工具列  
下表顯示移轉工具列命令：  
  
|按鈕|函數|  
|------|--------|  
|**建立報表**|將轉換至選取的 DB2 物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法，然後建立報表，其中顯示已成功的轉換。<br /><br />此命令會停用，除非 DB2 中繼資料總管 中選取的物件。|  
|**將結構描述轉換**|將轉換至選取的 DB2 物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]物件。<br /><br />此命令會停用，除非 DB2 中繼資料總管 中選取的物件。|  
|**將資料移轉**|將資料從 DB2 資料庫移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 執行此命令之前，您必須將轉換的 DB2 結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]結構描述，然後載入到物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br />此命令會停用，除非 DB2 中繼資料總管 中選取的物件。|  
|**停止**|停止目前的處理序。|  
  
### <a name="menus"></a>功能表  
下表顯示的 SSMA 功能表。  
  
|功能表|描述|  
|----|-----------|  
|**檔案**|包含用來處理專案、 連接至 DB2，以及連接到命令[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**編輯**|包含用來尋找和使用的詳細資料頁面中，例如複製的文字命令[!INCLUDE[tsql](../../includes/tsql-md.md)]從 [SQL 詳細資料] 窗格。 也包含**管理書籤**選項，其中您可以在此處看到一份現有的書籤。 您可以使用對話方塊右側的按鈕，來管理書籤。|  
|**[檢視]**|包含**同步處理中繼資料瀏覽器**命令。 會同步處理之間 DB2 中繼資料總管 的物件和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料總管。 也包含命令，以顯示和隱藏**輸出**並**錯誤清單**窗格和選項**配置**來管理配置。|  
|**工具**|包含命令來建立報表，並將物件和資料移轉。 也提供存取權**全域設定**並**專案設定**對話方塊。|  
|**說明**|提供存取至 SSMA 協助和**關於** 對話方塊。|  
  
### <a name="output-pane-and-error-list-pane"></a>輸出窗格和 [錯誤清單] 窗格  
**檢視** 功能表提供切換可見性的 輸出 窗格和 錯誤清單 窗格的命令：  
  
-   [輸出] 窗格會顯示在物件轉換、 物件同步處理和資料移轉期間從 SSMA 的狀態訊息。  
  
-   [錯誤清單] 窗格會顯示錯誤、 警告和參考用訊息，可排序的清單中。  
  
## <a name="see-also"></a>另請參閱  
[將 DB2 資料移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[使用者介面參考&#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  

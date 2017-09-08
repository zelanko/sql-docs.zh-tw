---
title: "開始使用 SSMA for Sybase (SybaseToSQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6a25db175cd6d67b71a0fc72bde969898e4bdadd
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="getting-started-with-ssma-for-sybase-sybasetosql"></a>開始使用 SSMA for Sybase (SybaseToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉小幫手 (SSMA) 的 Sybase 可讓您快速 Sybase Adaptive Server Enterprise (ASE) 資料庫將結構描述轉換至[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的結構描述上傳到產生的結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，並將資料從 Sybase ASE 來移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
本主題介紹安裝程序，並可協助您熟悉 SSMA 使用者介面。  
  
## <a name="installing-and-licensing-ssma"></a>安裝與授權 SSMA  
若要使用 SSMA，您先必須 SSMA 用戶端程式上安裝的 Sybase ASE 的來源執行個體和目標執行個體都可以存取的電腦[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 若要使用伺服器端資料移轉，您必須安裝延伸模組組件和至少一個 Sybase 提供者 （OLE DB 或 ADO.NET） 正在執行的電腦上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 這些元件支援的資料移轉和 Sybase ASE 系統函數的模擬。 如需安裝指示，請參閱[安裝 SSMA for Sybase &#40;SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md).  
  
若要啟動 SSMA，按一下**啟動**，指向**所有程式**，指向 **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉小幫手 for Sybase**，，然後選取  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]移轉小幫手 for Sybase**。 第一次您啟動 SSMA，授權的對話方塊隨即出現。 您必須使用 Windows Live ID，才能使用 SSMA 授權 SSMA。 授權的指示是使用中的安裝指示[安裝 SSMA for Sybase 用戶端 &#40;SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)主題。  
  
## <a name="ssma-for-sybase-user-interface"></a>SSMA for Sybase 使用者介面  
SSMA 會安裝並授權之後，您可以將 Sybase ASE 資料庫移轉至使用 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 它有助於熟悉 SSMA 使用者介面在開始之前。 下圖顯示 SSMA，包括中繼資料瀏覽器、 中繼資料、 工具列、 輸出窗格中，以及錯誤清單窗格的使用者介面：  
  
![SSMA for Sybase 使用者介面](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SSMA for Sybase 使用者介面")  
  
若要啟動移轉，您必須先建立新的專案。 然後，您會連接到 Sybase ASE。 成功連接之後，ASE Sybase 資料庫的階層會出現在 Sybase 中繼資料總管。 您可以執行工作，例如 Sybase 中繼資料總管 中的以滑鼠右鍵按一下物件建立評估轉換至的報表，然後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 您也可以執行這些工作，透過工具列和功能表。  
  
您也必須連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 成功連接之後，階層[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫將會出現在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管。 在轉換至 Sybase ASE 結構描述之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 結構描述中，選取那些已轉換的結構描述中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管，然後載入將結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
載入轉換後的結構描述之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure，您可以返回 Sybase 中繼資料總管 並將資料從 Sybase ASE 資料庫到移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫。  
  
如需這些工作和執行方式的詳細資訊，請參閱[將 Sybase ASE 資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md).  
  
下列章節說明 SSMA 使用者介面的功能。  
  
### <a name="metadata-explorers"></a>中繼資料瀏覽器  
SSMA 包含兩個中繼資料瀏覽器瀏覽和 Sybase ASE 上執行的動作和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 資料庫。  
  
#### <a name="sybase-metadata-explorer"></a>Sybase 中繼資料總管  
Sybase 中繼資料總管會顯示 Sybase ASE 來源執行個體上資料庫的相關資訊。  
  
藉由使用 Sybase 中繼資料總管，您可以執行下列工作：  
  
-   瀏覽每個資料庫中的資料表。  
  
-   選取轉換的物件，然後將轉換的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的語法。 如需詳細資訊，請參閱[轉換 Sybase ASE 資料庫物件 &#40;SybaseToSQL &#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
-   選取資料移轉的物件，然後將資料從這些物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 如需詳細資訊，請參閱[移轉 Sybase ASE 資料插入 SQL Server-Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md).  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server 或 SQL Azure 中繼資料總管  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure 中繼資料總管 會顯示資訊的執行個體或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 當您連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure、 SSMA 擷取有關該執行個體的中繼資料，並將它儲存在專案檔。  
  
您可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管] 選取 [已轉換的 Sybase ASE 資料庫物件，並再載入 （同步處理） 的執行個體將那些物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。  
  
如需詳細資訊，請參閱[載入轉換資料庫物件到 SQL Server &#40;SybaseToSQL &#41;](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md).  
  
### <a name="metadata"></a>中繼資料  
右邊的每個中繼資料總管 會描述所選的物件的索引標籤。 例如，如果您在 Sybase 中繼資料總管 中選取資料表，六個索引標籤會出現：**資料表**， **SQL**，**類型對應**，**資料、 屬性**和**報表**。 **報表**索引標籤包含的資訊，才建立包含所選的物件的報表。 如果您選取的資料表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管 會顯示三個索引標籤：**資料表**， **SQL**，和**資料**。  
  
大部分的中繼資料設定為唯讀。 不過，您可以將修改下列中繼資料：  
  
-   Sybase 中繼資料總管，在您可以改變程序及型別對應。 轉換結構描述之前，應該進行這些變更。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管，您可以改變[!INCLUDE[tsql](../../includes/tsql_md.md)]預存程序。 載入結構描述之前，應該進行這些變更[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
在 [中繼資料總管] 中所做的變更會反映在專案中繼資料，不在來源或目標資料庫中。  
  
### <a name="toolbars"></a>工具列  
SSMA 會有兩個工具列： 專案工具列和移轉工具列。  
  
#### <a name="the-project-toolbar"></a>[專案] 工具列  
[專案] 工具列包含處理專案、 連接到 Sybase ASE 和連接到按鈕[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 這些按鈕類似命令上**檔案**功能表。  
  
#### <a name="migration-toolbar"></a>移轉工具列  
移轉工具列包含下列命令：  
  
|按鈕|函數|  
|----------|------------|  
|**建立報表**|將轉換至選取的 Sybase ASE 物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]語法，然後建立報表來顯示如何成功轉換。<br /><br />Sybase 中繼資料總管 中選取物件時，才使用此命令。|  
|**轉換結構描述**|將轉換至選取的 Sybase ASE 物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 物件。<br /><br />Sybase 中繼資料總管 中選取物件時，才使用此命令。|  
|**將資料移轉**|將資料從 Sybase ASE 資料庫遷移[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。 執行此命令之前，您必須將 Sybase 結構描述，以轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的結構描述，然後載入物件到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。<br /><br />Sybase 中繼資料總管 中選取物件時，才使用此命令。|  
|**停止**|停止目前的程序，例如將轉換物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 的語法。|  
  
### <a name="menus"></a>功能表  
SSMA 會包含下列功能表。  
  
|功能表|Description|  
|--------|---------------|  
|**檔案**|包含用來處理專案、 連接到 Sybase ASE 以及連接到命令[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure。|  
|**編輯**|包含用來尋找及處理的詳細資料頁面中，例如，將複製的文字命令[!INCLUDE[tsql](../../includes/tsql_md.md)]從 [SQL 詳細資料] 窗格。 也包含**管理書籤**選項，您可以在此處看到一份現有書籤。 您可以使用對話方塊右側的按鈕，來管理這些書籤。|  
|**檢視**|包含**同步處理中繼資料瀏覽器**命令。 這會同步處理的物件之間 Sybase 中繼資料總管和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 SQL Azure 中繼資料總管。 還會包含命令來顯示和隱藏**輸出**和**錯誤清單**窗格和選項**配置**來管理配置。|  
|**工具**|包含命令來建立報表、 匯出資料，以及將物件和資料移轉。 也提供存取**通用設定**和**專案設定**對話方塊。|  
|**測試人員**|包含建立測試案例、 檢視測試結果和資料庫備份的管理命令的命令。|  
|**說明**|提供存取至 SSMA 協助和**有關** 對話方塊。|  
  
### <a name="output-pane-and-error-list-pane"></a>輸出窗格和 [錯誤清單] 窗格  
**檢視**功能表提供命令來切換可見性的 [輸出] 窗格和 [錯誤清單] 窗格：  
  
-   [輸出] 窗格會顯示物件轉換、 同步處理物件和資料移轉期間從 SSMA 的狀態訊息。  
  
-   [錯誤清單] 窗格會顯示錯誤、 警告和參考用訊息的清單中，您可以排序。  
  
## <a name="see-also"></a>另請參閱  
[Sybase ASE 將資料庫移轉至 SQL Server-Azure SQL DB &#40;SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[使用者介面參考 &#40;SybaseToSQL &#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  


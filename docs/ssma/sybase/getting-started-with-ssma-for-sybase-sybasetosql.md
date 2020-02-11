---
title: SSMA for SAP ASE （SybaseToSQL）的消費者入門 |Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: f07f230f52fee5707084c01060e92220b35cb75c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029120"
---
# <a name="getting-started-with-ssma-for-sap-ase-sybasetosql"></a>SSMA for SAP ASE （SybaseToSQL）的消費者入門
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移轉小幫手（SSMA） for SAP ASE 可讓您快速將 SAP 調適型伺服器 Enterprise （ASE） [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫架構轉換成或 Azure SQL Database 架構、將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產生的架構上傳至或 Azure SQL Database，以及[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將資料從 SAP ASE 遷移至或 Azure SQL Database。  
  
本主題將介紹安裝過程，並協助您熟悉 SSMA 使用者介面。  
  
## <a name="installing-and-licensing-ssma"></a>安裝和授權 SSMA  
若要使用 SSMA，您必須先在可存取 SAP ASE 的來源實例和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database 的目標實例的電腦上安裝 SSMA 用戶端程式。 若要使用伺服器端資料移轉，您必須在執行的電腦上安裝延伸模組套件和至少一個 SAP ASE 提供者（OLE DB 或 ADO.NET） [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這些元件支援資料移轉和 SAP ASE 系統函數的模擬。 如需安裝指示，請參閱[安裝 SSMA FOR SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)。  
  
若要開始 SSMA，請按一下 [**開始**]，指向 [**所有程式**]，指向** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [針對 sybase 移轉小幫手**]，然後選取** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [針對 sybase 移轉小幫手**]。 當您第一次啟動 SSMA 時，[授權] 對話方塊會隨即出現。 您必須先使用 Windows Live ID 授權 SSMA，才能使用 SSMA。 授權指示隨附于安裝[SSMA For Sybase Client &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)主題中的安裝指示。  
  
## <a name="ssma-for-sap-ase-user-interface"></a>適用于 SAP ASE 使用者介面的 SSMA  
安裝並授權 SSMA 之後，您可以使用 SSMA 將 SAP ASE 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database。 在開始之前，最好先熟悉 SSMA 的使用者介面。 下圖顯示 SSMA 的使用者介面，包括 [中繼資料流覽程式]、[中繼資料]、[工具列]、[輸出] 窗格和 [錯誤清單] 窗格：  
  
![適用于 SAP ASE 使用者介面的 SSMA](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "適用于 SAP ASE 使用者介面的 SSMA")  
  
若要開始進行遷移，您必須先建立新的專案。 然後，連接到 SAP ASE。 成功連接之後，會在 Sybase Metadata Explorer 中顯示 SAP ASE 資料庫的階層。 接著，您可以用滑鼠右鍵按一下 Sybase Metadata Explorer 中的物件來執行工作，例如建立可評估[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]轉換為或 Azure SQL Database 的報表。 您也可以透過工具列和功能表來執行這些工作。  
  
您也必須連接到的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例或 Azure SQL Database。 成功連線之後，或 Azure SQL 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的階層會出現在或 SQL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure 中繼資料 Explorer 中。 將 SAP ASE 架構轉換為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database 架構之後，請在或 SQL Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料 Explorer 中選取那些已轉換的架構，然後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將架構載入或 Azure SQL Database。  
  
將已轉換的架構載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database 之後，您可以回到 Sybase 中繼資料瀏覽器，並將資料從 SAP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ASE 資料庫移轉至或 Azure SQL 資料庫。  
  
如需這些工作和如何執行這些工作的詳細資訊，請參閱[將 SAP ASE 資料庫移轉至 SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)。  
  
下列各節說明 SSMA 使用者介面的功能。  
  
### <a name="metadata-explorers"></a>中繼資料流覽  
SSMA 包含兩個中繼資料瀏覽器，可在 SAP ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL 資料庫上流覽及執行動作。  
  
#### <a name="sybase-metadata-explorer"></a>Sybase 中繼資料瀏覽器  
Sybase Metadata Explorer 會顯示 SAP ASE 之來源實例上的資料庫相關資訊。  
  
藉由使用 Sybase Metadata Explorer，您可以執行下列工作：  
  
-   流覽每個資料庫中的資料表。  
  
-   選取要轉換的物件，然後將物件轉換為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database 語法。 如需詳細資訊，請參閱將[SAP ASE 資料庫物件轉換 &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)。  
  
-   選取 [資料移轉的物件]，然後將這些物件的資料移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至或 Azure SQL Database。 如需詳細資訊，請參閱將[SAP ASE 資料移轉至 SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md)。  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server 或 SQL Azure 中繼資料 Explorer  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料 Explorer 會顯示實例或 Azure SQL Database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的相關資訊。 當您連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database 的實例時，SSMA 會抓取該實例的中繼資料，並將它儲存在專案檔中。  
  
您可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料瀏覽器來選取已轉換的 SAP ASE 資料庫物件，然後將這些物件載入（同步處理[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ）至實例或 Azure SQL Database。  
  
如需詳細資訊，請參閱將已[轉換的資料庫物件載入 SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md)。  
  
### <a name="metadata"></a>中繼資料  
每個 [中繼資料 explorer] 的右邊是描述所選物件的索引標籤。 例如，如果您在 [Sybase 中繼資料瀏覽器] 中選取資料表，則會出現六個索引標籤：**資料表**、 **SQL**、**類型對應**、**資料**、**屬性**和**報表**。 只有在您建立包含所選物件的報表之後，[**報表**] 索引標籤才會包含資訊。 如果您在或 SQL Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中繼資料 Explorer 中選取資料表，則會出現三個索引標籤：**資料表**、 **SQL**和**資料**。  
  
大部分的中繼資料設定都是唯讀的。 不過，您可以改變下列中繼資料：  
  
-   在 Sybase 中繼資料瀏覽器中，您可以改變程式和類型對應。 請在轉換架構之前進行這些變更。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料瀏覽器中，您[!INCLUDE[tsql](../../includes/tsql-md.md)]可以改變預存程式的。 在您將架構載入之前，請先[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]進行這些變更。  
  
在中繼資料 explorer 中所做的變更會反映在專案中繼資料中，而不是在來源或目標資料庫中。  
  
### <a name="toolbars"></a>工具列  
SSMA 有兩個工具列： [專案] 工具列和 [遷移] 工具列。  
  
#### <a name="the-project-toolbar"></a>專案工具列  
[專案] 工具列包含用來處理專案、連接到 SAP ASE，以及連接至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database 的按鈕。 這些**按鈕與 [檔案] 功能表上**的命令類似。  
  
#### <a name="the-migration-toolbar"></a>遷移工具列  
[遷移] 工具列包含下列命令：  
  
|按鈕|函式|  
|----------|------------|  
|**建立報表**|將選取的 SAP ASE 物件轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成語法，然後建立報表來顯示轉換成功的程度。<br /><br />只有在 [Sybase 中繼資料瀏覽器] 中選取物件時，才能使用此命令。|  
|**轉換架構**|將選取的 SAP ASE 物件轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]為或 Azure SQL Database 物件。<br /><br />只有在 [Sybase 中繼資料瀏覽器] 中選取物件時，才能使用此命令。|  
|**遷移資料**|將資料從 SAP ASE 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database。 執行此命令之前，您必須先將 SAP ASE 架構轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database 架構，然後將物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database。<br /><br />只有在 [Sybase 中繼資料瀏覽器] 中選取物件時，才能使用此命令。|  
|**停止**|停止目前的進程，例如將物件轉換為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database 語法。|  
  
### <a name="menus"></a>功能表  
SSMA 包含下列功能表：  
  
|功能表|描述|  
|--------|---------------|  
|**檔案**|包含用來處理專案、連接到 SAP ASE，以及連接至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database 的命令。|  
|**編輯**|包含在詳細資料頁面中尋找和使用文字的命令，例如從 [ [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL 詳細資料] 窗格複製。 同時包含 [**管理書簽**] 選項，您可以在其中查看現有書簽的清單。 您可以使用對話方塊右側的按鈕來管理書簽。|  
|**檢視**|包含**同步處理中繼資料**的流覽命令。 這會同步處理 Sybase Metadata Explorer 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 SQL Azure 中繼資料瀏覽器之間的物件。 也包含用來顯示和隱藏 [**輸出**] 和 [**錯誤清單**] 窗格的命令，以及用來管理版面配置的選項**版面**配置。|  
|**工具**|包含用來建立報表、匯出資料，以及遷移物件和資料的命令。 也會提供 [**全域設定**] 和 [**專案設定**] 對話方塊的存取權。|  
|**測試人員**|包含用來建立測試案例、查看測試結果和資料庫備份管理命令的命令。|  
|**説明**|提供 SSMA 說明和 [**關於**] 對話方塊的存取權。|  
  
### <a name="output-pane-and-error-list-pane"></a>輸出窗格和錯誤清單窗格  
[ **View** ] 功能表提供命令來切換 [輸出] 窗格和 [錯誤清單] 窗格的可見度：  
  
-   [輸出] 窗格會在物件轉換、物件同步處理和資料移轉期間，顯示來自 SSMA 的狀態訊息。  
  
-   [錯誤清單] 窗格會在可排序的清單中顯示錯誤、警告和參考用訊息。  
  
## <a name="see-also"></a>另請參閱  
[將 SAP ASE 資料庫移轉至 SQL Server Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[&#40;SybaseToSQL&#41;的使用者介面參考](../../ssma/sybase/user-interface-reference-sybasetosql.md)  

---
title: SSMA for DB2 的消費者入門（DB2ToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0eab4f23e342c95d83baa70dd03aba2f5d4bc8d1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67989645"
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>SSMA for DB2 的消費者入門（DB2ToSQL）
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移轉小幫手（SSMA） for DB2 可讓您快速地將 DB2 資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架構轉換成架構，將產生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的架構上傳至， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並將資料從 DB2 遷移至。  
  
本主題將介紹安裝過程，並協助您熟悉 SSMA 使用者介面。  
  
## <a name="installing-ssma"></a>安裝 SSMA  
若要使用 SSMA，您必須先在可同時存取來源 DB2 資料庫和目標實例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦上安裝 SSMA 用戶端程式。 執行之電腦上的 DB2 OLEDB 提供者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這些元件支援資料移轉和 DB2 系統函數的模擬。 如需安裝指示，請參閱[安裝 SSMA FOR DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)。  
  
若要開始 SSMA，請按一下 [**開始**]，指向 [**所有程式**]，指向 [ ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移轉小幫手 for db2**]，然後按一下** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [移轉小幫手 for db2**]。  
  
## <a name="ssma-for-db2-user-interface"></a>SSMA for DB2 使用者介面  
安裝 SSMA 之後，您可以使用 SSMA 將 DB2 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在開始之前，最好先熟悉 SSMA 的使用者介面。 下圖顯示 SSMA 的使用者介面，包括 [中繼資料流覽程式]、[中繼資料]、[工具列]、[輸出] 窗格和 [錯誤清單] 窗格：  
  
![SSMA 使用者介面](../../ssma/db2/media/ssma_db2_ui.png "SSMA 使用者介面")  
  
若要開始進行遷移，您必須先建立新的專案。 然後，連接到 DB2 資料庫。 成功連接之後，db2 架構將會出現在 DB2 Metadata Explorer 中。 接著，您可以用滑鼠右鍵按一下 DB2 Metadata Explorer 中的物件來執行工作，例如建立可[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]評估轉換的報表。 您也可以使用工具列和功能表來執行這些工作。  
  
您也必須連接到的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例。 成功連接之後，[中繼資料流覽[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]器] 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會顯示資料庫的階層。 將 DB2 架構轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架構之後，請在 [中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]瀏覽器] 中選取那些已轉換的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架構，然後將架構與同步處理。  
  
使用同步處理已轉換的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架構之後，您可以返回 Db2 Metadata Explorer，並將資料從 db2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架構遷移至資料庫。  
  
如需這些工作和如何執行這些工作的詳細資訊，請參閱[將 DB2 資料庫移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)。  
  
下列各節說明 SSMA 使用者介面的功能。  
  
### <a name="metadata-explorers"></a>中繼資料流覽  
SSMA 包含兩個中繼資料瀏覽器，可在 DB2 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫上流覽及執行動作。  
  
#### <a name="db2-metadata-explorer"></a>DB2 中繼資料 Explorer  
DB2 Metadata Explorer 會顯示 DB2 架構的相關資訊。 藉由使用 DB2 Metadata Explorer，您可以執行下列工作：  
  
-   流覽每個架構中的物件。  
  
-   選取要轉換的物件，然後將物件轉換成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]語法。 如需詳細資訊，請參閱將[DB2 架構轉換 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)。  
  
-   選取資料表以進行資料移轉，然後將這些資料表中的資料移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]至。 如需詳細資訊，請參閱[將 DB2 資料庫移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)。  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server 中繼資料 Explorer  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][中繼資料瀏覽器] 會顯示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例的相關資訊。 當您連接到的實例時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，SSMA 會抓取該實例的中繼資料，並將它儲存在專案檔中。  
  
您可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [中繼資料瀏覽器] 選取已轉換的 DB2 資料庫物件，然後將這些物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與的實例同步處理。  
  
### <a name="metadata"></a>中繼資料  
每個 [中繼資料 explorer] 的右邊是描述所選物件的索引標籤。 例如，如果您在 DB2 Metadata Explorer 中選取資料表，則會出現六個索引標籤：**資料表**、 **SQL**、**類型對應、報表**、**屬性**和**資料**。 只有在建立包含所選物件的報表之後，[**報表**] 索引標籤才會包含資訊。 如果您在 [中繼資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]瀏覽器] 中選取資料表，則會出現三個索引標籤：**資料表**、 **SQL**和**資料**。  
  
大部分的中繼資料設定都是唯讀的。 不過，您可以改變下列中繼資料：  
  
-   在 DB2 Metadata Explorer 中，您可以改變程式和類型對應。 若要轉換已改變的程式和類型對應，請在轉換架構之前進行變更。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [中繼資料] Explorer 中， [!INCLUDE[tsql](../../includes/tsql-md.md)]您可以改變預存程式的。 若要在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]查看這些變更，請先進行這些變更，再[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將架構載入中。  
  
在中繼資料 explorer 中所做的變更會反映在專案中繼資料中，而不是在來源或目標資料庫中。  
  
### <a name="toolbars"></a>工具列  
SSMA 有兩個工具列： [專案] 工具列和 [遷移] 工具列。  
  
#### <a name="the-project-toolbar"></a>專案工具列  
[專案] 工具列包含用來處理專案、連接到 DB2，以及連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的按鈕。 這些**按鈕與 [檔案] 功能表上**的命令類似。  
  
#### <a name="migration-toolbar"></a>遷移工具列  
下表顯示遷移工具列命令：  
  
|按鈕|函式|  
|------|--------|  
|**建立報表**|將選取的 DB2 物件轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成語法，然後建立報表來顯示轉換成功的程度。<br /><br />除非在 DB2 Metadata Explorer 中選取物件，否則會停用此命令。|  
|**轉換架構**|將選取的 DB2 物件轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]成物件。<br /><br />除非在 DB2 Metadata Explorer 中選取物件，否則會停用此命令。|  
|**遷移資料**|將資料從 DB2 資料庫移轉至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 執行此命令之前，您必須先將 DB2 架構轉換為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架構，然後將物件載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。<br /><br />除非在 DB2 Metadata Explorer 中選取物件，否則會停用此命令。|  
|**停止**|停止目前的進程。|  
  
### <a name="menus"></a>功能表  
下表顯示 [SSMA] 功能表。  
  
|功能表|描述|  
|----|-----------|  
|**檔案**|包含用來處理專案、連接到 DB2，以及連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的命令。|  
|**編輯**|包含在詳細資料頁面中尋找和使用文字的命令，例如從 [ [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL 詳細資料] 窗格複製。 同時包含 [**管理書簽**] 選項，您可以在其中看到現有書簽的清單。 您可以使用對話方塊右側的按鈕來管理書簽。|  
|**檢視**|包含**同步處理中繼資料**的流覽命令。 這會同步處理 DB2 Metadata Explorer 與[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Metadata explorer 之間的物件。 也包含用來顯示和隱藏**輸出**和**錯誤清單**窗格的命令，以及用來管理版面配置的選項**版面**配置。|  
|**工具**|包含用來建立報表和遷移物件和資料的命令。 也會提供 [**全域設定**] 和 [**專案設定**] 對話方塊的存取權。|  
|**說明**|提供 SSMA 說明和 [**關於**] 對話方塊的存取權。|  
  
### <a name="output-pane-and-error-list-pane"></a>輸出窗格和錯誤清單窗格  
[ **View** ] 功能表提供命令來切換 [輸出] 窗格和 [錯誤清單] 窗格的可見度：  
  
-   [輸出] 窗格會在物件轉換、物件同步處理和資料移轉期間，顯示來自 SSMA 的狀態訊息。  
  
-   [錯誤清單] 窗格會在可排序清單中顯示錯誤、警告和參考用訊息。  
  
## <a name="see-also"></a>另請參閱  
[將 DB2 資料移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[&#40;DB2ToSQL&#41;的使用者介面參考](../../ssma/db2/user-interface-reference-db2tosql.md)  
  

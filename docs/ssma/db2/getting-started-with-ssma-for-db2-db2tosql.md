---
description: '消費者入門與 SSMA for DB2 (DB2ToSQL) '
title: 消費者入門與 SSMA for DB2 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7cb317fc73f32a8795fe5ce4e5be9af776edf938
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454257"
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>消費者入門與 SSMA for DB2 (DB2ToSQL) 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) for DB2 可讓您將 DB2 資料庫架構快速轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 架構、將產生的架構上傳至， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並將資料從 DB2 遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
本主題將介紹安裝程式，並協助您熟悉 SSMA 的使用者介面。  
  
## <a name="installing-ssma"></a>安裝 SSMA  
若要使用 SSMA，您必須先將 SSMA 用戶端程式安裝在可存取來源 DB2 資料庫和目標實例的電腦上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 正在執行之電腦上的 DB2 OLEDB 提供者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這些元件支援資料移轉和 DB2 系統函數的模擬。 如需安裝指示，請參閱 [安裝 SSMA FOR DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md)。  
  
若要開始 SSMA，請按一下 [**開始**]，指向 [**所有程式**]，指向 [ ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for db2**]，然後按一下 [ ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for db2**]。  
  
## <a name="ssma-for-db2-user-interface"></a>SSMA for DB2 消費者介面  
安裝 SSMA 之後，您可以使用 SSMA 將 DB2 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 在開始之前，它有助於先熟悉 SSMA 的使用者介面。 下圖顯示 SSMA 的使用者介面，包括 [中繼資料流覽程式]、[中繼資料]、[工具列]、[輸出窗格] 和 [錯誤清單] 窗格：  
  
![SSMA 使用者介面](../../ssma/db2/media/ssma_db2_ui.png "SSMA 使用者介面")  
  
若要開始遷移，您必須先建立新專案。 然後，您會連接到 DB2 資料庫。 成功連接之後，DB2 架構將會出現在 DB2 Metadata Explorer 中。 然後，您可以用滑鼠右鍵按一下 DB2 Metadata Explorer 中的物件來執行工作，例如建立評估轉換的報表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您也可以使用工具列和功能表來執行這些工作。  
  
您也必須連接到的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 連接成功後，[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中繼資料瀏覽器] 中會出現資料庫階層。 在您將 DB2 架構轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 架構之後，請在 [中繼資料瀏覽器] 中選取那些轉換過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的架構，然後將架構與同步處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
在同步處理已轉換的架構之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，您可以返回 Db2 中繼資料瀏覽器，並將資料從 DB2 架構遷移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中。  
  
如需這些工作及其執行方式的詳細資訊，請參閱 [將 DB2 資料庫移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)。  
  
下列各節說明 SSMA 使用者介面的功能。  
  
### <a name="metadata-explorers"></a>中繼資料流覽  
SSMA 包含兩個中繼資料瀏覽器，以流覽和執行 DB2 和資料庫上的動作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
#### <a name="db2-metadata-explorer"></a>DB2 中繼資料瀏覽器  
DB2 中繼資料瀏覽器會顯示 DB2 架構的相關資訊。 藉由使用 DB2 Metadata Explorer，您可以執行下列工作：  
  
-   流覽每個架構中的物件。  
  
-   選取物件進行轉換，然後將物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語法。 如需詳細資訊，請參閱 [轉換 DB2 架構 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md)。  
  
-   選取資料表以進行資料移轉，然後將這些資料表中的資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱 [將 DB2 資料庫移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)。  
  
#### <a name="sql-server-metadata-explorer"></a>SQL Server 中繼資料瀏覽器  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [中繼資料瀏覽器] 會顯示實例的相關資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 當您連接到的實例時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，SSMA 會抓取該實例的中繼資料，並將其儲存在專案檔中。  
  
您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [中繼資料瀏覽器] 來選取轉換的 DB2 資料庫物件，然後將這些物件與的實例同步處理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
### <a name="metadata"></a>中繼資料  
每個中繼資料瀏覽器右邊都有描述所選物件的索引標籤。 例如，如果您在 [DB2 中繼資料瀏覽器] 中選取資料表，則會出現六個索引標籤： **資料表**、 **SQL**、 **類型對應、報表**、 **屬性**和 **資料**。 [ **報表** ] 索引標籤只有在您建立包含所選物件的報表之後，才會包含資訊。 如果您在 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中繼資料瀏覽器] 中選取資料表，則會顯示三個索引標籤： **資料表**、 **SQL**和 **資料**。  
  
大部分的中繼資料設定都是唯讀的。 不過，您可以變更下列中繼資料：  
  
-   在 DB2 中繼資料瀏覽器中，您可以變更程式和類型對應。 若要轉換更改的程式和類型對應，請在轉換架構之前進行變更。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [中繼資料瀏覽器] 中，您可以改變 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程式的。 若要在中查看這些變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請先進行這些變更，然後再將架構載入中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
在中繼資料瀏覽器中所做的變更會反映在專案中繼資料中，不會反映在來源或目標資料庫中。  
  
### <a name="toolbars"></a>工具列  
SSMA 有兩個工具列： [專案] 工具列和 [遷移] 工具列。  
  
#### <a name="the-project-toolbar"></a>專案工具列  
[專案] 工具列包含使用專案、連接至 DB2 以及連接至的按鈕 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這些按鈕 **類似于 [檔案] 功能表上** 的命令。  
  
#### <a name="migration-toolbar"></a>遷移工具列  
下表顯示遷移工具列命令：  
  
|按鈕|函式|  
|------|--------|  
|**建立報表**|將選取的 DB2 物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語法，然後建立報表來顯示轉換的成功程度。<br /><br />除非在 DB2 Metadata Explorer 中選取物件，否則會停用此命令。|  
|**轉換架構**|將選取的 DB2 物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件。<br /><br />除非在 DB2 Metadata Explorer 中選取物件，否則會停用此命令。|  
|**遷移資料**|將資料從 DB2 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 執行此命令之前，您必須先將 DB2 架構轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 架構，然後將物件載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。<br /><br />除非在 DB2 Metadata Explorer 中選取物件，否則會停用此命令。|  
|**停止**|停止目前的進程。|  
  
### <a name="menus"></a>功能表  
下表顯示 [SSMA] 功能表。  
  
|功能表|描述|  
|----|-----------|  
|**檔案**|包含用來處理專案、連接至 DB2 以及連接至的命令 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**編輯**|包含在詳細資料頁面中尋找和使用文字的命令，例如 [!INCLUDE[tsql](../../includes/tsql-md.md)] 從 SQL 詳細資料窗格複製。 也包含 [ **管理書簽** ] 選項，您可以在其中查看現有書簽的清單。 您可以使用對話方塊右邊的按鈕來管理書簽。|  
|**檢視**|包含 **同步處理中繼資料** 流覽命令。 這會同步處理 DB2 Metadata Explorer 與 Metadata Explorer 之間的物件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 也包含用來顯示和隱藏 [ **輸出** ] 和 [ **錯誤清單** ] 窗格的命令，以及用來管理配置的選項 **版面** 配置。|  
|**工具**|包含用來建立報表和遷移物件和資料的命令。 也提供 [ **全域設定** ] 和 [ **專案設定** ] 對話方塊的存取權。|  
|**說明**|提供 SSMA 說明和 [ **關於** ] 對話方塊的存取權。|  
  
### <a name="output-pane-and-error-list-pane"></a>[輸出窗格] 和 [錯誤清單] 窗格  
[ **View** ] 功能表會提供命令來切換 [輸出] 窗格和 [錯誤清單] 窗格的可見度：  
  
-   [輸出] 窗格會顯示物件轉換、物件同步處理和資料移轉期間的 SSMA 狀態訊息。  
  
-   [錯誤清單] 窗格會在可排序的清單中顯示錯誤、警告和資訊訊息。  
  
## <a name="see-also"></a>另請參閱  
[將 DB2 資料移轉至 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[消費者介面參考 &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  

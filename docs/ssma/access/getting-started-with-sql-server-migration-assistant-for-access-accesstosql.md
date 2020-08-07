---
title: 開始使用 SQL Server 移轉小幫手進行存取 |Microsoft Docs
description: 開始使用 SSMA，將 Access 資料庫物件轉換成 SQL Server 或 Azure SQL Database 物件、上傳產生的物件，以及遷移資料。
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
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: d622396e9e650aa3e9fc1b3855e1dfc1634bc34e
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938767"
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>開始使用 SQL Server 移轉小幫手存取 (AccessToSQL) 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移轉小幫手 (SSMA) 進行存取，可讓您快速地將 Access 資料庫物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 物件、將產生的物件上傳至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database，以及將資料從存取權遷移至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。 如有需要，您也可以將存取資料表連結到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 資料表，以便繼續使用現有的存取前端應用程式， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。  
  
本主題將介紹安裝程式，並協助您熟悉 SSMA 使用者介面。  
  
## <a name="installing-ssma"></a>安裝 SSMA  
若要使用 SSMA，您必須先在可存取您想要遷移之資料庫的電腦上，以及或 Azure SQL Database 的目標實例上安裝 SSMA 用戶端程式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需安裝指示，請參閱[安裝 SQL Server 移轉小幫手以存取 &#40;AccessToSQL&#41;](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md)。  
  
若要開始 SSMA，請按一下 [**開始**]，指向 [**所有程式**]，指向 [ **SQL Server 移轉小幫手進行存取**]，然後選取 [ **SQL Server 移轉小幫手進行存取**]。  
  
## <a name="using-ssma"></a>使用 SSMA  
安裝 SSMA 之後，在使用工具將 Access 資料庫移轉至或 Azure SQL Database 之前，它有助於熟悉 SSMA 使用者介面 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 SSMA 使用者介面，包括中繼資料流覽、中繼資料、工具列、輸出窗格和 [錯誤清單] 窗格，如下圖所示：  
  
![SSMA for Access 圖形化使用者介面](../../ssma/access/media/ssmaforaccessgui.gif "SSMA for Access 圖形化使用者介面")  
  
若要開始進行遷移，請建立新的專案，然後加入 Access 資料庫以存取 Metadata Explorer。 接著，您可以用滑鼠右鍵按一下 [存取中繼資料瀏覽器] 中的物件來執行下列工作：
- 將 Access 資料庫物件的清查匯出至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。
- 建立可評估轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 的報表。
- 將存取架構轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 架構。

您也可以使用工具列和功能表來執行這些工作。  
  
您也必須連接到的實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 成功連接之後， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中繼資料瀏覽器] 中會顯示資料庫的階層。 將存取架構轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 架構之後，您可以在 [中繼資料瀏覽器] 中選取那些已轉換的架構 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然後將架構載入至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
如果您已從 [新增專案] 對話方塊的 [遷移至] 下拉式清單中選取 [Azure SQL Database]，則必須連接到 Azure SQL Database。 成功連接之後，Azure SQL Database 資料庫的階層會出現在 Azure SQL Database Metadata Explorer 中。 將存取架構轉換成 Azure SQL Database 架構之後，您可以在 Azure SQL Database 中繼資料 Explorer 中選取那些已轉換的架構，然後將架構載入中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
將已轉換的架構載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 之後，您可以返回存取中繼資料瀏覽器，並將資料從 Access 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 資料庫。 如有必要，您也可以將 Access 資料表連結至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 資料表。  
  
如需這些工作和如何執行這些工作的詳細資訊，請參閱下列主題：  
  
-   [準備 Access 資料庫以進行遷移](preparing-access-databases-for-migration-accesstosql.md)  
  
-   [將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
-   [將存取應用程式連結至 SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
下列各節說明 SSMA 使用者介面的功能。  
  
### <a name="metadata-explorers"></a>中繼資料流覽  
SSMA 包含兩個中繼資料瀏覽器，可讓您用來流覽和執行存取和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 資料庫上的動作。  
  
#### <a name="access-metadata-explorer"></a>存取中繼資料總管  
存取中繼資料瀏覽器會顯示已加入至專案之 Access 資料庫的相關資訊。 當您加入 Access 資料庫時，SSMA 會抓取該資料庫的中繼資料，也就是 Access Metadata Explorer 中可用的中繼資料。  
  
您可以使用 [存取中繼資料瀏覽器] 執行下列工作：  
  
-   流覽每個 Access 資料庫中的資料表。  
  
-   選取要轉換的物件，並將物件轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 語法。 如需詳細資訊，請參閱[轉換 Access 資料庫物件](converting-access-database-objects-accesstosql.md)。  
  
-   選取要資料移轉的物件，並將這些物件的資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱將[存取資料移轉至 SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)。  
  
-   連結和取消連結存取和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
#### <a name="sql-server-or-azure-sql-database-metadata-explorer"></a>SQL Server 或 Azure SQL Database 中繼資料 Explorer  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或 Azure SQL Database 中繼資料 Explorer 會顯示實例或 Azure SQL Database 的相關資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 當您連接到或 Azure SQL Database 的實例時 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，SSMA 會抓取該實例的中繼資料，並將它儲存在專案檔中。  
  
您可以使用 [SQL Server] 或 [Azure SQL Database 中繼資料瀏覽器] 選取已轉換的 Access 資料庫物件，並載入 (將這些物件) 同步處理到實例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。  
  
如需詳細資訊，請參閱將已[轉換的資料庫物件載入 SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)。  
  
### <a name="metadata"></a>中繼資料  
每個 [中繼資料 explorer] 的右邊是描述所選物件的索引標籤。 例如，如果您在 [存取中繼資料瀏覽器] 中選取資料表，則會出現四個索引標籤：**資料表**、**類型對應**、**屬性**和**資料**。 如果您在 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中繼資料瀏覽器] 中選取資料表，則會出現三個索引標籤：**資料表**、 **SQL**和**資料**。  
  
大部分的中繼資料設定都是唯讀的。 不過，您可以改變下列中繼資料：  
  
-   在 [存取中繼資料 Explorer] 中，您可以改變型別對應。 請務必在建立報表或轉換架構之前進行這些變更。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [中繼資料] Explorer 中，您可以在 [**資料表**] 索引標籤上修改資料表和索引屬性。在將架構載入之前，請先進行這些變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需詳細資訊，請參閱[轉換 Access 資料庫物件](converting-access-database-objects-accesstosql.md)。  
  
### <a name="toolbars"></a>工具列  
SSMA 有兩個工具列： [專案] 工具列和 [遷移] 工具列。  
  
#### <a name="the-project-toolbar"></a>專案工具列  
[專案] 工具列包含用於處理專案、加入 Access 資料庫檔案，以及連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 的按鈕。 這些**按鈕與 [檔案] 功能表上**的命令類似。  
  
#### <a name="the-migration-toolbar"></a>遷移工具列  
[遷移] 工具列包含下列命令：  
  
|按鈕|函式|  
|----------|------------|  
|**轉換、載入和移轉**|會轉換 Access 資料庫、將轉換的物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database，並將資料移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database，全都在一個步驟中進行。|  
|**建立報表**|將選取的存取架構轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 語法，然後建立報表以顯示轉換成功的程度。<br /><br />只有在 [存取中繼資料瀏覽器] 中選取物件時，才能使用此命令。|  
|**轉換架構**|將選取的存取架構轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 架構。<br /><br />只有在 [存取中繼資料瀏覽器] 中選取物件時，才能使用此命令。|  
|**遷移資料**|將資料從 Access 資料庫移轉至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。 執行此命令之前，您必須先將存取架構轉換成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 架構，然後將物件載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。<br /><br />只有在 [存取中繼資料瀏覽器] 中選取物件時，才能使用此命令。|  
|**停止**|停止目前的進程，例如將物件轉換為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 語法。|  
  
### <a name="menus"></a>功能表  
SSMA 包含下列功能表：  
  
|功能表|描述|  
|--------|---------------|  
|**檔案**|包含用於遷移 Wizard 的命令、使用專案、加入和移除 Access 資料庫檔案，以及連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database。|  
|**編輯**|包含在詳細資料頁面中尋找和使用文字的命令，例如 [!INCLUDE[tsql](../../includes/tsql-md.md)] 從 [SQL 詳細資料] 窗格複製。 若要開啟 [**管理書簽**] 對話方塊，請在 [編輯] 功能表上，按一下 [管理書簽]。 在對話方塊中，您會看到現有書簽的清單。 您可以使用對話方塊右側的按鈕來管理書簽。|  
|**檢視**|包含**同步處理中繼資料**的流覽命令。 這會同步存取中繼資料瀏覽器與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 Azure SQL Database 中繼資料瀏覽器之間的物件。 也包含用來顯示和隱藏 [**輸出**] 和 [**錯誤清單**] 窗格的命令，以及要使用版面配置來管理的選項**版面**配置。|  
|**工具**|包含用來建立報表、匯出資料、遷移物件和資料、連結資料表，以及提供全域和專案設定對話方塊存取的命令。|  
|**說明**|提供 SSMA 說明和 [**關於**] 對話方塊的存取權。|  
  
### <a name="output-pane-and-error-list-pane"></a>輸出窗格和錯誤清單窗格  
[ **View** ] 功能表提供命令來切換 [輸出] 窗格和 [錯誤清單] 窗格的可見度：  
  
-   [輸出] 窗格會在物件轉換、物件同步處理和資料移轉期間，顯示來自 SSMA 的狀態訊息。  
  
-   [錯誤清單] 窗格會在可排序的清單中顯示錯誤、警告和參考用訊息。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  

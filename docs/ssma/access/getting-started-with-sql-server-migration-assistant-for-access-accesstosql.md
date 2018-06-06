---
title: 開始使用 SQL Server 移轉小幫手存取 |Microsoft 文件
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-access
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 450057d8167423b07a729a4bd05c65e67a533b37
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>開始使用 SQL Server 移轉小幫手存取 (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 移轉小幫手 (SSMA) 的存取可讓您快速地轉換到存取資料庫物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 物件上傳到產生的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB、 從存取移轉資料和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 如果有必要，您也可以將連結來存取資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 資料表，好讓您可以繼續使用現有的存取前端應用程式與[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。  
  
本主題介紹的安裝程序，並可協助您熟悉 SSMA 使用者介面。  
  
## <a name="installing-ssma"></a>安裝 SSMA  
若要使用 SSMA，您首先必須安裝 SSMA 用戶端程式可以存取您想要移轉的這兩個資料庫的電腦和目標執行個體的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 如需安裝指示，請參閱[安裝 SQL Server 移轉小幫手存取&#40;AccessToSQL&#41;](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md)。  
  
若要啟動 SSMA，按一下**啟動**，指向**所有程式**，指向**SQL Server 移轉小幫手存取**，然後選取**SQL Server 移轉小幫手存取**。  
  
## <a name="using-ssma"></a>使用 SSMA  
在安裝之後 SSMA，它有助於熟悉 SSMA 使用者介面將 Access 資料庫移轉至使用此工具之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 SSMA 使用者介面，包括中繼資料瀏覽器、 中繼資料、 工具列、 輸出窗格中，以及錯誤清單 窗格會顯示在下圖中：  
  
![SSMA for Access 圖形化使用者介面](../../ssma/access/media/ssmaforaccessgui.gif "SSMA for Access 圖形化使用者介面")  
  
若要啟動移轉，建立新的專案，然後再加入 Access 資料庫來存取中繼資料總管。 您可以再以滑鼠右鍵按一下執行工作，例如存取中繼資料總管 中的物件：
- 匯出到存取資料庫物件的清查[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。
- 建立報表以評估轉換為[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。
- 轉換到存取結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 結構描述。

您也可以使用工具列和功能表來執行這些工作。  
  
您也必須連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 成功連接之後，階層[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫會出現在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管。 在轉換到存取結構描述之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]結構描述，您可以選取這些轉換的結構描述中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管，然後載入將結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
如果您選取 Azure SQL DB 從移轉至新專案 對話方塊中的下拉式清單中，您必須連接到 Azure SQL DB。 成功連接之後，Azure SQL DB 資料庫的階層會出現在 Azure SQL DB 中繼資料總管。 您將存取結構描述轉換至 Azure SQL DB 結構描述之後，您可以這些轉換的結構描述總管中選取 Azure SQL DB 中繼資料，並再載入將結構描述[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
載入轉換後的結構描述之後[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB，您可以返回存取中繼資料總管 並將資料從到 Access 資料庫移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 資料庫。 如果有必要，您也可以將連結來存取資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 資料表。  
  
如需有關這些工作和執行方式的詳細資訊，請參閱下列主題：  
  
-   [準備移轉的 Access 資料庫](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
-   [將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
-   [連結到 SQL Server 存取應用程式](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)  
  
下列章節說明 SSMA 使用者介面的功能。  
  
### <a name="metadata-explorers"></a>中繼資料瀏覽器  
SSMA 包含兩個中繼資料總管可讓您瀏覽並執行動作的存取和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 資料庫。  
  
#### <a name="access-metadata-explorer"></a>存取中繼資料總管  
存取中繼資料總管 會顯示已加入至專案存取資料庫的相關資訊。 當您新增 Access 資料庫時，SSMA 會擷取有關該資料庫中，也就是在存取中繼資料總管 中可用的中繼資料的中繼資料。  
  
您可以使用存取中繼資料總管 來執行下列工作：  
  
-   瀏覽每個存取資料庫中的資料表。  
  
-   選取轉換的物件，並將轉換的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]語法。 如需詳細資訊，請參閱[轉換來存取資料庫物件](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)。  
  
-   選取資料移轉的物件，並將這些物件的資料移轉[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需詳細資訊，請參閱[移轉至 SQL Server 的存取資料](http://msdn.microsoft.com/f3b18af7-1af0-499d-a00d-a0af94895625)。  
  
-   連結和取消連結存取和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料表。  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 或 Azure SQL DB 中繼資料總管  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Azure SQL DB 中繼資料總管 會顯示資訊的執行個體或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 當您連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB、 SSMA 擷取有關該執行個體的中繼資料，並將它儲存在專案檔。  
  
您可以使用 SQL Server 或 Azure SQL DB 中繼資料總管] 選取 [已轉換的存取資料庫物件及載入 （同步處理） 的執行個體將那些物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。  
  
如需詳細資訊，請參閱[載入轉換的資料庫物件至 SQL Server](http://msdn.microsoft.com/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba)。  
  
### <a name="metadata"></a>中繼資料  
右邊的每個中繼資料總管 會描述所選的物件的索引標籤。 例如，如果您在存取中繼資料總管 中選取資料表，四個索引標籤會出現：**資料表**，**類型對應**，**屬性**，和**資料**。 如果您選取的資料表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管 中，三個索引標籤會出現：**資料表**， **SQL**，和**資料**。  
  
大部分的中繼資料設定為唯讀。 不過，您可以將修改下列中繼資料：  
  
-   在存取中繼資料總管，您可能會改變型別對應。 請確定您建立報表，或將結構描述轉換之前進行這些變更。  
  
-   在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中繼資料總管 中，您可以變更資料表和索引的屬性上**資料表** 索引標籤。進行這些變更，再將結構描述載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如需詳細資訊，請參閱[轉換來存取資料庫物件](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c)。  
  
### <a name="toolbars"></a>工具列  
SSMA 會有兩個工具列： 專案工具列和移轉工具列。  
  
#### <a name="the-project-toolbar"></a>[專案] 工具列  
[專案] 工具列包含按鈕，以使用專案、 加入 Access 資料庫檔案，並連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 這些按鈕類似命令上**檔案**功能表。  
  
#### <a name="the-migration-toolbar"></a>[移轉] 工具列  
移轉工具列包含下列命令：  
  
|按鈕|函數|  
|----------|------------|  
|**轉換、載入和移轉**|將 Access 資料庫轉換、 載入轉換的物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL 資料庫，並移轉資料到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或在一個步驟中，所有的 Azure SQL DB。|  
|**建立報表**|將選取的存取結構描述轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 語法，然後建立報表來顯示如何成功轉換。<br /><br />只有在存取中繼資料總管 中選取物件時，此命令才能使用。|  
|**轉換結構描述**|將選取的存取結構描述轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 結構描述。<br /><br />只有在存取中繼資料總管 中選取物件時，此命令才能使用。|  
|**將資料移轉**|若要在 Access 資料庫移轉資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。 執行此命令之前，您必須將存取結構描述，以轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 結構描述，然後載入物件到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。<br /><br />只有在存取中繼資料總管 中選取物件時，此命令才能使用。|  
|**停止**|停止目前的程序，例如將轉換物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 語法。|  
  
### <a name="menus"></a>功能表  
SSMA 會包含下列功能表：  
  
|功能表|Description|  
|--------|---------------|  
|**檔案**|「 移轉精靈 」，使用專案中，加入和移除存取資料庫檔案，以及連接到包含指令[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB。|  
|**編輯**|包含用來尋找及處理的詳細資料頁面中，例如，將複製的文字命令[!INCLUDE[tsql](../../includes/tsql_md.md)]從 [SQL 詳細資料] 窗格。 若要開啟**管理書籤**對話方塊中的，編輯 功能表中，按一下 管理書籤。 在對話方塊中，您會看到一份現有書籤。 您可以使用對話方塊右側的按鈕，來管理這些書籤。|  
|**檢視**|包含**同步處理中繼資料瀏覽器**命令。 這會同步處理存取中繼資料總管 之間的物件和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]或 Azure SQL DB 中繼資料總管。 還會包含命令來顯示和隱藏**輸出**和**錯誤清單**窗格和選項**配置**管理版面配置。|  
|**工具**|包含命令來建立報表、 匯出的資料、 物件和資料移轉，連結資料表，並提供存取全域和專案設定 對話方塊。|  
|**說明**|提供存取至 SSMA 協助和**有關** 對話方塊。|  
  
### <a name="output-pane-and-error-list-pane"></a>輸出窗格和 [錯誤清單] 窗格  
**檢視**功能表提供命令來切換可見性的 [輸出] 窗格和 [錯誤清單] 窗格：  
  
-   [輸出] 窗格會顯示物件轉換、 同步處理物件和資料移轉期間從 SSMA 的狀態訊息。  
  
-   [錯誤清單] 窗格會顯示錯誤、 警告和參考用訊息的清單中，您可以排序。  
  
## <a name="see-also"></a>另請參閱  
[將 Access 資料庫移轉至 SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

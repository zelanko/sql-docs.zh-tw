---
title: 開始使用 SSMA for MySQL (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Getting started, MySQL metadata explorer
- Getting started, SQL Server or SQL Azure metadata explorer
- Getting started,Installing and licensing
ms.assetid: 8ebfa061-be6f-4a07-923f-8dc832a82f70
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1ae91f90bf601e4ef17ae2f363260dbb47a2822e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187144"
---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>開始使用 SSMA for MySQL (MySQLToSQL)
SQL Server Migration Assistant (SSMA) 適用於 MySQL 可讓您快速將 MySQL 資料庫結構描述轉換成 SQL Server 或 Azure SQL DB 結構描述、 將產生的結構描述上傳到 SQL Server 或 Azure SQL DB，並將資料從 MySQL 移轉至 SQL Server 或 Azure SQL DB。  
  
本主題介紹安裝程序，並接著可幫助您熟悉 SSMA 使用者介面。  
  
## <a name="installing-ssma"></a>安裝 SSMA  
若要使用 SSMA，您首先必須安裝 SSMA 用戶端程式可以存取 MySQL 資料庫，以及 SQL Server 或 Azure SQL DB 的目標執行個體的電腦上。 然後，執行 SSMA 的用戶端程式的電腦上安裝 MySQL 提供者 （MySQL ODBC 5.1 驅動程式 （受信任））。 如需安裝指示，請參閱[安裝 SSMA for MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
若要啟動 SSMA，請按一下**開始**，指向**所有程式**，指向**SQL Server Migration Assistant for MySQL**，然後按一下  **SQL Server 移轉適用於 MySQL 的助理**。  
  
## <a name="ssma-for-mysql-user-interface"></a>SSMA for MySQL 使用者介面  
SSMA 會安裝並授權之後，您可以使用 SSMA 將 MySQL 資料庫移轉至 SQL Server 或 Azure SQL DB。 最好先熟悉 SSMA 使用者介面在開始之前。 下圖顯示的 SSMA，包括中繼資料瀏覽器、 中繼資料、 工具列、 輸出 窗格中，以及錯誤清單 窗格中的使用者介面：  
  
![SSMA for MySql 圖形化使用者介面](../../ssma/mysql/media/ssmaformysqlgui.gif "SSMA for MySql 圖形化使用者介面")  
  
若要啟動移轉，您必須：  
  
1.  建立新專案。  
  
2.  連線到 MySQL 資料庫。  
  
3.  成功連線之後，MySQL 結構描述會出現在 [MySQL 中繼資料總管]。 以滑鼠右鍵按一下物件，在執行工作，例如 MySQL 中繼資料總管 中的建立報表，評估 SQL Server/Azure SQL db 的轉換。  
  
您也可以使用工具列和功能表來執行這些工作。  
  
您也必須連接到 SQL Server 的執行個體。 成功連線之後，SQL Server 資料庫的階層會出現在 SQL Server 中繼資料總管。 您將 MySQL 結構描述轉換至 SQL Server 結構描述之後，這些已轉換的結構描述總管中選取 SQL Server 中繼資料，並與 SQL Server，然後同步處理結構描述。  
  
如果您選取從移轉的 Azure SQL DB，以在 [新增專案] 對話方塊中的下拉式清單中，您必須連接到 Azure SQL DB。 成功連線之後，Azure SQL DB 資料庫的階層會出現在 Azure SQL DB 中繼資料總管。 您將 MySQL 結構描述轉換至 Azure SQL DB 結構描述之後，這些已轉換的結構描述總管中選取 Azure SQL DB 中繼資料，並與 Azure SQL DB，然後同步處理結構描述。  
  
您與 SQL Server 或 Azure SQL DB 同步處理已轉換的結構描述之後，您可以返回 [MySQL 中繼資料總管]，然後將資料從 MySQL 結構描述移轉至 SQL Server 或 Azure SQL DB 資料庫。  
  
如需有關這些工作，以及如何執行這些的詳細資訊，請參閱[將 MySQL 資料庫移轉至 SQL Server-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)。  
  
下列各節說明的 SSMA 使用者介面的功能。  
  
### <a name="metadata-explorers"></a>中繼資料瀏覽器  
SSMA 會包含兩個中繼資料瀏覽器，瀏覽和 MySQL 和 SQL Server 資料庫上執行動作。  
  
### <a name="mysql-metadata-explorer"></a>MySQL 中繼資料總管  
MySQL 中繼資料總管 會顯示 MySQL 結構描述的相關資訊。 藉由使用 MySQL 中繼資料總管，您可以執行下列工作：  
  
-   瀏覽每個結構描述中的物件。  
  
-   選取轉換的物件，然後將物件轉換成 SQL Server 的語法。 如需詳細資訊，請參閱 <<c0> [ 轉換 MySQL 資料庫&#40;MySQLToSQL&#41;</c0>](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   選取的資料移轉的資料表，然後從那些資料表的資料移轉至 SQL Server。 如需詳細資訊，請參閱 <<c0> [ 移轉到 SQL Server-Azure SQL DB 的 MySQL 資料&#40;MySQLToSQL&#41;</c0>](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 或 Azure SQL DB 中繼資料總管  
SQL Server 或 Azure SQL DB 中繼資料總管 會顯示 SQL Server 或 Azure SQL DB 的執行個體的相關資訊。 當您連接到 SQL Server 或 Azure SQL DB 的執行個體時，SSMA 會擷取該執行個體相關的中繼資料，並將它儲存在專案檔中。  
  
您可以使用此中繼資料總管 來選取已轉換的 MySQL 資料庫物件，並與 SQL Server 或 Azure SQL DB 的執行個體，然後同步處理這些物件。  
  
如需詳細資訊，請參閱[同步處理 (從 mysql 移轉至 SQL Server / Azure SQL DB)](https://msdn.microsoft.com/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>中繼資料  
右邊的每個中繼資料總管 會描述所選的物件的索引標籤。 例如，如果您在 [MySQL 中繼資料總管] 中選取資料表，就會出現九個索引標籤：**表格**， **SQL**，**類型對應**，**資料**，**設定**，**字元集對應**，**SQL 模式**，**屬性**，並**報表**。 **報表** 索引標籤包含的資訊，建立報表之後，就會包含選取的物件。 如果您在 SQL Server 中繼資料總管 中選取資料表，則會出現三個索引標籤：**表格**， **SQL**並**資料**。  
  
大部分的中繼資料設定是唯讀的。 不過，您可以變更下列中繼資料：  
  
-   在 MySQL 中繼資料總管 中，您可能會改變對應的類型，對應的字元集，SQL 模式。 若要變更的型別對應或字元集對應或 SQL 模式轉換，進行變更，再將結構描述的轉換。  
  
-   在 [SQL Server 中繼資料總管] 中，您可以變更資料表索引標籤上的資料表和索引的屬性。若要查看這些變更的 SQL Server，請在之前的結構描述載入 SQL Server 進行這些變更。  
  
在 [中繼資料總管] 中所做的變更會反映專案中繼資料，不在來源或目標資料庫中。  
  
### <a name="toolbars"></a>工具列  
SSMA 會有兩個工具列： 專案工具列和移轉工具列。  
  
### <a name="the-project-toolbar"></a>[專案] 工具列  
[專案] 工具列包含使用專案、 連接至 MySQL，以及連接到 SQL Server 或 Azure SQL DB 的按鈕。 這些按鈕上類似的命令**檔案**功能表。  
  
### <a name="migration-toolbar"></a>移轉工具列  
下表顯示移轉工具列命令：  
  
|||  
|-|-|  
|**Button**|**函數**|  
|**建立報表**|將選取的 MySQL 物件轉換成 SQL Server 或 Azure SQL DB 的物件，並接著會建立報表，其中顯示已成功的轉換。<br /><br />此命令會停用，除非在 MySQL 中繼資料總管 中選取的物件。|  
|**將結構描述轉換**|將選取的 MySQL 物件轉換成 SQL Server 或 Azure SQL DB 的物件。<br /><br />此命令會停用，除非在 MySQL 中繼資料總管 中選取的物件。|  
|**將資料移轉**|將資料從 MySQL 資料庫移轉至 SQL Server 或 Azure SQL DB。 執行此命令之前，您必須將 MySQL 結構描述轉換成 SQL Server 或 Azure SQL DB 結構描述，並接著將物件載入至 SQL Server 或 Azure SQL DB。<br /><br />此命令會停用，除非在 MySQL 中繼資料總管 中選取的物件。|  
|**停止**|停止目前的處理序。|  
  
### <a name="menus"></a>功能表  
下表顯示的 SSMA 功能表。  
  
|||  
|-|-|  
|**功能表**|**說明**|  
|**檔案**|包含用來處理專案、 連接至 MySQL，以及連接到 SQL Server 或 Azure SQL DB 命令。|  
|**編輯**|包含用來尋找和處理的詳細資料頁面中的文字命令。 若要開啟 **管理書籤**對話方塊中的，在 編輯 功能表上按一下 管理書籤。 在對話方塊中，您會看到一份現有的書籤。 您可以使用對話方塊右側的按鈕，來管理書籤。|  
|**[檢視]**|包含**同步處理中繼資料瀏覽器**命令。 會同步處理 MySQL 中繼資料總管，SQL Server 或 Azure SQL DB 中繼資料總管 之間的物件。 也包含命令，以顯示和隱藏**輸出**並**錯誤清單**窗格和選項**配置**來管理與配置。|  
|**工具**|包含如何建立報表、 將結構描述轉換、 從資料庫重新整理、 移轉物件和資料，和將儲存為指令碼的命令。 也提供存取權**全域設定]、 [預設專案設定**並**專案設定**對話方塊。|  
|**說明**|提供存取至 SSMA 協助和**關於** 對話方塊。|  
  
### <a name="output-pane-and-error-list-pane"></a>輸出窗格和 [錯誤清單] 窗格  
**檢視** 功能表提供切換可見性的 輸出 窗格和 錯誤清單 窗格的命令：  
  
-   [輸出] 窗格會顯示在物件轉換、 物件同步處理和資料移轉期間從 SSMA 的狀態訊息。  
  
-   [錯誤清單] 窗格會顯示錯誤、 警告和參考用訊息，可排序的清單中。  
  
## <a name="see-also"></a>另請參閱  
[使用者介面參考&#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[將 MySQL 資料移轉到 SQL Server-Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  

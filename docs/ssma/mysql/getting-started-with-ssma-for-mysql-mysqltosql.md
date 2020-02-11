---
title: SSMA for MySQL （MySQLToSQL）的消費者入門 |Microsoft Docs
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
ms.openlocfilehash: 5a1adb6d9354dc870c11fab0a68f6c92e704ebfb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67984543"
---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>開始使用 SSMA for MySQL (MySQLToSQL)
適用于 MySQL 的 SQL Server 移轉小幫手（SSMA）可讓您快速將 MySQL 資料庫架構轉換成 SQL Server 或 Azure SQL DB 架構、將產生的架構上傳至 SQL Server 或 Azure SQL DB，以及將資料從 MySQL 遷移至 SQL Server 或 Azure SQL DB。  
  
本主題將介紹安裝過程，並協助您熟悉 SSMA 使用者介面。  
  
## <a name="installing-ssma"></a>安裝 SSMA  
若要使用 SSMA，您必須先在可存取來源 MySQL 資料庫和 SQL Server 或 Azure SQL DB 的目標實例的電腦上安裝 SSMA 用戶端程式。 然後，在執行 SSMA 用戶端程式的電腦上安裝 MySQL 提供者（MySQL ODBC 5.1 驅動程式（受信任））。 如需安裝指示，請參閱[安裝 SSMA For MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
若要開始 SSMA，請按一下 [**開始**]，指向 [**所有程式**]，指向 [**適用于 mysql 的 SQL Server 移轉小幫手**]，然後按一下 [**適用于 mysql SQL Server 移轉小幫手**]。  
  
## <a name="ssma-for-mysql-user-interface"></a>SSMA for MySQL 使用者介面  
安裝並授權 SSMA 之後，您可以使用 SSMA 將 MySQL 資料庫遷移至 SQL Server 或 Azure SQL DB。 在開始之前，最好先熟悉 SSMA 的使用者介面。 下圖顯示 SSMA 的使用者介面，包括 [中繼資料流覽程式]、[中繼資料]、[工具列]、[輸出] 窗格和 [錯誤清單] 窗格：  
  
![SSMA for MySql 圖形化使用者介面](../../ssma/mysql/media/ssmaformysqlgui.gif "SSMA for MySql 圖形化使用者介面")  
  
若要開始進行遷移，您必須：  
  
1.  建立新專案。  
  
2.  連接到 MySQL 資料庫。  
  
3.  成功連線之後，MySQL 架構會出現在 MySQL Metadata Explorer 中。 以滑鼠右鍵按一下 [MySQL Metadata Explorer 中的物件] 來執行工作，例如建立報表來評估 SQL Server/Azure SQL DB 的轉換。  
  
您也可以使用工具列和功能表來執行這些工作。  
  
您也必須連接到 SQL Server 的實例。 成功連接之後，SQL Server 資料庫的階層會出現在 SQL Server Metadata Explorer 中。 將 MySQL 架構轉換成 SQL Server 架構之後，請在 SQL Server Metadata Explorer 中選取那些已轉換的架構，然後將架構與 SQL Server 同步處理。  
  
如果您已從 [新增專案] 對話方塊中的 [遷移至] 下拉式清單選取 [Azure SQL DB]，則必須連線至 Azure SQL DB。 成功連線之後，azure SQL DB 資料庫的階層會出現在 Azure SQL DB 中繼資料 Explorer 中。 將 MySQL 架構轉換成 Azure SQL DB 架構之後，請在 Azure SQL DB 中繼資料 Explorer 中選取那些已轉換的架構，然後將架構與 Azure SQL DB 同步處理。  
  
當您使用 SQL Server 或 Azure SQL DB 同步處理已轉換的架構之後，您可以返回 MySQL 中繼資料瀏覽器，並將資料從 MySQL 架構遷移到 SQL Server 或 Azure SQL DB 資料庫。  
  
如需這些工作和如何執行這些工作的詳細資訊，請參閱[將 MySQL 資料庫遷移至 SQL Server-AZURE SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)。  
  
下列各節說明 SSMA 使用者介面的功能。  
  
### <a name="metadata-explorers"></a>中繼資料流覽  
SSMA 包含兩個中繼資料瀏覽器，可在 MySQL 和 SQL Server 資料庫上流覽及執行動作。  
  
### <a name="mysql-metadata-explorer"></a>MySQL 中繼資料 Explorer  
MySQL 中繼資料 Explorer 會顯示 MySQL 架構的相關資訊。 藉由使用 MySQL 中繼資料瀏覽器，您可以執行下列工作：  
  
-   流覽每個架構中的物件。  
  
-   選取要轉換的物件，然後將物件轉換成 SQL Server 語法。 如需詳細資訊，請參閱將[MySQL 資料庫轉換 &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   選取資料表以進行資料移轉，然後將這些資料表中的資料移轉至 SQL Server。 如需詳細資訊，請參閱將[MySQL 資料移轉至 SQL Server-AZURE SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server 或 Azure SQL DB 中繼資料 Explorer  
SQL Server 或 Azure SQL DB 中繼資料 Explorer 會顯示 SQL Server 或 Azure SQL DB 實例的相關資訊。 當您連接到 SQL Server 或 Azure SQL DB 的實例時，SSMA 會抓取該實例的中繼資料，並將其儲存在專案檔中。  
  
您可以使用此中繼資料瀏覽器來選取已轉換的 MySQL 資料庫物件，然後將這些物件與 SQL Server 或 Azure SQL DB 的實例同步處理。  
  
如需詳細資訊，請參閱[同步處理（MySQL 至 SQL Server/AZURE SQL DB）](https://msdn.microsoft.com/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>中繼資料  
每個 [中繼資料 explorer] 的右邊是描述所選物件的索引標籤。 例如，如果您在 [MySQL 中繼資料瀏覽器] 中選取資料表，則會出現九個索引標籤：**資料表**、 **SQL**、**類型對應**、**資料**、**設定**、**字元集對應**、 **SQL 模式**、**屬性**和**報表**。 只有在建立包含所選物件的報表之後，[**報表**] 索引標籤才會包含資訊。 如果您在 SQL Server 中繼資料 Explorer 中選取資料表，則會出現三個索引標籤：**資料表**、 **SQL**和**資料**。  
  
大部分的中繼資料設定都是唯讀的。 不過，您可以改變下列中繼資料：  
  
-   在 MySQL 中繼資料瀏覽器中，您可以改變類型對應、字元集對應、SQL 模式。 若要轉換已改變的類型對應或字元集對應或 SQL 模式，請在轉換架構之前進行變更。  
  
-   在 SQL Server 中繼資料瀏覽器中，您可以在 [資料表] 索引標籤上變更資料表和索引屬性。若要在 SQL Server 中查看這些變更，請在將架構載入 SQL Server 之前進行這些變更。  
  
在中繼資料 explorer 中所做的變更會反映在專案中繼資料中，而不是在來源或目標資料庫中。  
  
### <a name="toolbars"></a>工具列  
SSMA 有兩個工具列： [專案] 工具列和 [遷移] 工具列。  
  
### <a name="the-project-toolbar"></a>專案工具列  
[專案] 工具列包含用來處理專案、連線至 MySQL，以及連接到 SQL Server 或 Azure SQL DB 的按鈕。 這些**按鈕與 [檔案] 功能表上**的命令類似。  
  
### <a name="migration-toolbar"></a>遷移工具列  
下表顯示遷移工具列命令：  
  
|||  
|-|-|  
|**按鈕**|**函數**|  
|**建立報表**|將選取的 MySQL 物件轉換成 SQL Server 或 Azure SQL DB 物件，然後建立報表來顯示轉換的成功程度。<br /><br />除非在 MySQL Metadata Explorer 中選取物件，否則會停用此命令。|  
|**轉換架構**|將選取的 MySQL 物件轉換成 SQL Server 或 Azure SQL DB 物件。<br /><br />除非在 MySQL Metadata Explorer 中選取物件，否則會停用此命令。|  
|**遷移資料**|將資料從 MySQL 資料庫遷移至 SQL Server 或 Azure SQL DB。 執行此命令之前，您必須先將 MySQL 架構轉換成 SQL Server 或 Azure SQL DB 架構，然後將物件載入 SQL Server 或 Azure SQL DB。<br /><br />除非在 MySQL Metadata Explorer 中選取物件，否則會停用此命令。|  
|**停止**|停止目前的進程。|  
  
### <a name="menus"></a>功能表  
下表顯示 [SSMA] 功能表。  
  
|||  
|-|-|  
|**功能表**|**說明**|  
|**檔案**|包含用來處理專案、連線至 MySQL，以及連接到 SQL Server 或 Azure SQL DB 的命令。|  
|**編輯**|包含在 [詳細資料] 頁面中尋找和使用文字的命令。 若要開啟 [**管理書簽**] 對話方塊，請按一下 [編輯] 功能表上的 [管理書簽]。 在對話方塊中，您會看到現有書簽的清單。 您可以使用對話方塊右側的按鈕來管理書簽。|  
|**檢視**|包含**同步處理中繼資料**的流覽命令。 這會在 MySQL Metadata Explorer 和 SQL Server 或 Azure SQL DB 中繼資料 Explorer 之間同步處理物件。 也包含用來顯示和隱藏 [**輸出**] 和 [**錯誤清單**] 窗格的命令，以及用來管理版面配置的選項**版面**配置。|  
|**工具**|包含用來建立報表、轉換架構、從資料庫重新整理、遷移物件和資料，以及另存為腳本的命令。 也提供 [**全域設定]、[預設專案設定**] 和 [**專案設定**] 對話方塊的存取權。|  
|**説明**|提供 SSMA 說明和 [**關於**] 對話方塊的存取權。|  
  
### <a name="output-pane-and-error-list-pane"></a>輸出窗格和錯誤清單窗格  
[ **View** ] 功能表提供命令來切換 [輸出] 窗格和 [錯誤清單] 窗格的可見度：  
  
-   [輸出] 窗格會在物件轉換、物件同步處理和資料移轉期間，顯示來自 SSMA 的狀態訊息。  
  
-   [錯誤清單] 窗格會在可排序清單中顯示錯誤、警告和參考用訊息。  
  
## <a name="see-also"></a>另請參閱  
[&#40;MySQLToSQL&#41;的使用者介面參考](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[將 MySQL 資料移轉至 SQL Server-Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  

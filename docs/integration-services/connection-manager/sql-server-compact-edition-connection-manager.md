---
title: SQL Server Compact Edition 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sqlmobileconnection.connection.f1
- sql13.dts.designer.sqlmobileconnection.all.f1
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9ee6d7483d90858563579ff9a9d92bcc44bd481b
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65728097"
---
# <a name="sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 連接管理員

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 連線管理員可讓封裝連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact 目的地會使用此連線管理員將資料載入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫。  
  
> [!NOTE]  
>  在 64 位元電腦上，您必須以 32 位元模式執行連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料來源的封裝。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用來連接到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact 資料來源的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 提供者只有提供 32 位元版本。  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 連接管理員的組態  
 當您將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 連線管理員加入封裝時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行階段解析為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 連接的連線管理員、設定連線管理員屬性，並將連線管理員加入封裝上的 **Connections** 集合。  
  
 連線管理員的 **ConnectionManagerType** 屬性會設為 **SQLMOBILE**。  
  
 您可以利用下列方式設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 連線管理員：  
  
-   提供指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫位置的連接字串。  
  
-   提供有密碼保護之資料庫的密碼。  
  
-   指定儲存資料庫的伺服器。  
  
-   指示是否在執行階段保留從連接管理員建立的連接。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="sql-server-compact-edition-connection-manager-editor-connection-page"></a>SQL Server Compact Edition 連接管理員編輯器 (連接頁面)
  使用 [SQL Server Compact Edition 連線管理員] 對話方塊，指定連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫的屬性。  
  
 若要深入了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Edition 連線管理員，請參閱 [SQL Server Compact Edition 連線管理員](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)。  
  
### <a name="options"></a>選項。  
 **輸入資料庫檔案名稱與路徑**  
 輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫的路徑與檔名。  
  
 **瀏覽**  
 使用 [選取 SQL Server Compact Edition 資料庫] 對話方塊，尋找所要的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫檔案。  
  
 **輸入資料庫密碼**  
 輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫的密碼。  
  
## <a name="sql-server-compact-edition-connection-manager-editor-all-page"></a>SQL Server Compact Edition 連接管理員編輯器 (全部頁面)
  使用 [SQL Server Compact Edition 連線管理員] 對話方塊，指定連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫的屬性。  
  
 若要深入了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Edition 連線管理員，請參閱 [SQL Server Compact Edition 連線管理員](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)。  
  
### <a name="options"></a>選項。  
 **AutoShrink 臨界值**  
 以百分比指定在執行自動壓縮處理序之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫允許的可用空間數量。  
  
 **預設鎖定擴大**  
 指定在嘗試擴大鎖定之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫要取得的資料庫鎖定數目。  
  
 **預設鎖定逾時**  
 指定交易等候鎖定的預設間隔，以毫秒為單位。  
  
 **排清間隔**  
 指定已認可交易將資料排清到磁碟機之間的間隔，以秒為單位。  
  
 **地區設定識別碼**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫的地區設定識別碼 (LCID)。  
  
 **緩衝區大小上限**  
 指定將資料排清到磁碟之前， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 使用的記憶體數量上限 (以 KB 為單位)。  
  
 **資料庫大小上限**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫的大小上限 (以 MB 為單位)。  
  
 **模式**  
 指定用來開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫的檔案模式。 此屬性的預設值為 [讀取寫入]。  
  
 模式選項有四個值，如下表所述。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**唯讀**|指定唯讀存取資料庫。|  
|**讀取寫入**|指定資料庫的讀取/寫入權限。|  
|**排除**|指定獨佔存取資料庫。|  
|**共用讀取**|指定其他使用者可同時讀取資料庫。|  
  
 **保存安全性資訊**  
 指定是否將安全性資訊當做連接字串的一部分傳回。 這個選項的預設值是 **False**。  
  
 **暫存檔目錄**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 暫存資料庫檔案的位置。  
  
 **資料來源**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫的名稱。  
  
 **密碼**  
 輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 資料庫的密碼。  
  

---
title: SQL Server Compact Edition 連線管理員編輯器（全部頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlmobileconnection.all.f1
helpviewer_keywords:
- SQL Server Compact Connection Manager Editor
ms.assetid: f9fbff4b-c502-44b3-8e7b-398d66e82206
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4ddfebf9f606a717eabbeeccbcf9fd79742f60dc
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421255"
---
# <a name="sql-server-compact-edition-connection-manager-editor-all-page"></a>SQL Server Compact Edition 連接管理員編輯器 (全部頁面)
  使用 [SQL Server Compact Edition 連線管理員]**** 對話方塊，指定連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 資料庫的屬性。  
  
 若要深入了解 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact Edition 連線管理員，請參閱 [SQL Server Compact Edition 連線管理員](connection-manager/sql-server-compact-edition-connection-manager.md)。  
  
## <a name="options"></a>選項  
 **AutoShrink 臨界值**  
 以百分比指定在執行自動壓縮處理序之前， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 資料庫允許的可用空間數量。  
  
 **預設鎖定擴大**  
 指定在嘗試擴大鎖定之前， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 資料庫要取得的資料庫鎖定數目。  
  
 **預設鎖定逾時**  
 指定交易等候鎖定的預設間隔，以毫秒為單位。  
  
 **排清間隔**  
 指定已認可交易將資料排清到磁碟機之間的間隔，以秒為單位。  
  
 **地區設定識別碼**  
 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 資料庫的地區設定識別碼 (LCID)。  
  
 **緩衝區大小上限**  
 指定將資料排清到磁碟之前， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 使用的記憶體數量上限 (以 KB 為單位)。  
  
 **資料庫大小上限**  
 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 資料庫的大小上限 (以 MB 為單位)。  
  
 **Mode**  
 指定用來開啟 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 資料庫的檔案模式。 此屬性的預設值為 [讀取寫入]****。  
  
 模式選項有四個值，如下表所述。  
  
|值|描述|  
|-----------|-----------------|  
|**唯讀**|指定唯讀存取資料庫。|  
|**讀寫**|指定資料庫的讀取/寫入權限。|  
|**排除**|指定獨佔存取資料庫。|  
|**共用讀取**|指定其他使用者可同時讀取資料庫。|  
  
 **保存安全性資訊**  
 指定是否將安全性資訊當做連接字串的一部分傳回。 這個選項的預設值是 **False**。  
  
 **暫存檔目錄**  
 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 暫存資料庫檔案的位置。  
  
 **資料來源**  
 指定 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 資料庫的名稱。  
  
 **密碼**  
 輸入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact 資料庫的密碼。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [SQL Server Compact Edition 連線管理員編輯器 &#40;連接頁面&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
  

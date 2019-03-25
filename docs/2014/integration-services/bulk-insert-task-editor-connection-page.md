---
title: 大量插入工作編輯器 （連接頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.bulkinserttask.connection.f1
helpviewer_keywords:
- Bulk Insert Task Editor
ms.assetid: 51252c20-8865-4ede-a3fd-bd73a968f47d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bf5d6f0a92b18cc41f74d068686c3c8c9589228a
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377246"
---
# <a name="bulk-insert-task-editor-connection-page"></a>大量插入工作編輯器 (連接頁面)
  使用 [大量插入工作編輯器] 對話方塊的 [連接] 頁面，即可指定大量插入作業的來源和目的地，以及要使用的格式。  
  
 若要了解如何使用大量插入，請參閱[大量插入工作](control-flow/bulk-insert-task.md)和[匯入或匯出資料的格式檔案 &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)。  
  
## <a name="options"></a>選項。  
 **[連接]**  
 在清單中選取 OLE DB 連線管理員，或按一下 [\<新增連接…>] 建立新的連接。  
  
 **相關主題：**[OLE DB 連線管理員](connection-manager/ole-db-connection-manager.md)，[設定 OLE DB 連接管理員](../../2014/integration-services/configure-ole-db-connection-manager.md)  
  
 **DestinationTable**  
 輸入目的地資料表或檢視的名稱，或在清單中選取資料表或檢視。  
  
 **格式**  
 選取大量插入的格式來源。 這個屬性具有下表中所列的選項。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**使用檔案**|選取包含格式規格的檔案。 選取此選項會顯示動態選項 [FormatFile]。|  
|**指定**|指定格式。 選取此選項會顯示動態選項`RowDelimiter`和`ColumnDelimiter`。|  
  
 **檔案**  
 在清單中選取檔案或一般檔案連線管理員，或按一下 [\<新增連接...>] 建立新的連接。  
  
 檔案位置相對於在此工作之連接管理員中指定的 SQL Server Database Engine。 SQL Server Database Engine 必須可以在伺服器上的本機硬碟，或透過 SQL Server 的共用或對應磁碟機，存取文字檔。 SSIS 執行階段無法存取檔案。  
  
 如果您使用一般檔案連接管理員存取來源檔案，則大量插入工作不會使用一般檔案連接管理員中指定的格式。 而「大量插入」工作會使用格式檔案中指定的格式，或工作之 RowDelimiter 和 ColumnDelimiter 屬性的值。  
  
 **相關主題：**[檔案連接管理員](connection-manager/file-connection-manager.md)，[檔案連線管理員編輯器](../../2014/integration-services/file-connection-manager-editor.md)，[一般檔案連線管理員](connection-manager/flat-file-connection-manager.md)，[一般檔案連接管理員編輯器 &#40;&#41; ](general-page-of-integration-services-designers-options.md)，[一般檔案連接管理員編輯器&#40;資料行頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)，[一般檔案連接管理員編輯器&#40;進階頁面&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)  
  
 **重新整理資料表**  
 重新整理資料表和檢視的清單。  
  
## <a name="format-dynamic-options"></a>格式動態選項  
  
### <a name="format--use-file"></a>格式 = 使用檔案  
 **FormatFile**  
 輸入格式檔案的路徑，或按一下省略符號按鈕 **(...)** 以尋找格式檔案。  
  
### <a name="format--specify"></a>格式 = 指定  
 `RowDelimiter`  
 指定來源檔案中的資料列分隔符號。 預設值是 [{CR}{LF}]。  
  
 `ColumnDelimiter`  
 指定來源檔案中的資料行分隔符號。 預設值是 [定位字元]。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [大量插入工作編輯器 &#40;一般頁面&#41;](../../2014/integration-services/bulk-insert-task-editor-general-page.md)   
 [大量插入工作編輯器 &#40;選項頁面&#41;](../../2014/integration-services/bulk-insert-task-editor-options-page.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [控制流程](control-flow/control-flow.md)  
  
  

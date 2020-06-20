---
title: CDC 來源 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.f1
ms.assetid: 99775608-e177-44ed-bb44-aaccb0f4f327
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e3452e504072188ea5f4bacf3fa6f10002335fb4
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84916638"
---
# <a name="cdc-source"></a>CDC 來源
  CDC 來源會從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 變更資料表中讀取變更資料的範圍，並將這些變更向下游傳遞至其他 SSIS 元件。  
  
 CDC 來源所讀取的變數資料範圍稱為 CDC 處理範圍，並且由目前資料流程啟動之前執行的 CDC 控制工作所決定。 CDC 處理範圍衍生自維護資料表群組之 CDC 處理狀態的封裝變數值。  
  
 CDC 來源會使用資料庫資料表、檢視或 SQL 陳述式，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中擷取資料。  
  
 CDC 來源使用下列組態：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ADO.NET 連接管理員，用以存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 資料庫。 如需設定 CDC 來源連接的詳細資訊，請參閱 [CDC 來源編輯器 &#40;連線管理員頁面&#41;](../cdc-source-editor-connection-manager-page.md)。  
  
-   啟用 CDC 的資料表。  
  
-   所選資料表的擷取執行個體名稱 (如果 more-than-one 存在)。  
  
-   變更處理模式。  
  
-   做為決定 CDC 處理範圍之依據的 CDC 狀態封裝變數名稱。 CDC 來源不會修改該變數。  
  
 CDC 來源傳回的資料與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cdc 函數**cdc. fn_cdc_get_all_changes_ \<capture-instance-name> **或 cdc 所傳回的資料相同。 **fn_cdc_get_net_changes_ \<capture-instance-name> ** （如果有的話）。 唯一的選擇性附加資料行是 **__$initial_processing** ，表示目前處理範圍是否可與資料表的初始載入重疊。 如需初始處理的詳細資訊，請參閱 [CDC 控制工作](../control-flow/cdc-control-task.md)。  
  
 CDC 來源有一個一般輸出和一個錯誤輸出。  
  
## <a name="error-handling"></a>錯誤處理  
 CDC 來源有錯誤輸出。 此元件的錯誤輸出包含下列輸出資料行：  
  
-   **錯誤碼**：此值一律為 -1。  
  
-   **錯誤資料行**：造成錯誤 (用於轉換錯誤) 的來源資料行。  
  
-   **錯誤資料列資料行**：造成錯誤的記錄資料。  
  
 根據錯誤行為設定，CDC 來源支援在錯誤輸出中傳回擷取程序期間發生的錯誤 (資料轉換、截斷)。 如需詳細資訊，請參閱 [CDC 來源編輯器 &#40;錯誤輸出頁面&#41;](../cdc-source-editor-error-output-page.md)。  
  
## <a name="data-type-support"></a>資料類型支援  
 Microsoft 的 CDC 來源元件支援所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，這些資料類型都會對應至正確的 SSIS 資料類型。  
  
## <a name="troubleshooting-the-cdc-source"></a>CDC 來源的疑難排解  
 以下包含 CDC 來源的疑難排解資訊。  
  
### <a name="use-this-script-to-isolate-problems-and-reproduce-them-in-sql-server-management-studio"></a>使用此指令碼來隔離問題，並在 SQL Server Management Studio 中重現問題。  
 CDC 來源作業是由叫用 CDC 來源之前執行的 CDC 控制工作作業所控制。 CDC 控制工作會準備 CDC 狀態封裝變數的值，以包含開始和結束 LSN。 它所執行的功能相當於下列指令碼：  
  
```  
use <cdc-enabled-database-name>  
               declare @start_lsn binary(10), @end_lsn binary(10)  
               set @start_lsn = sys.fn_cdc_increment_lsn(  
                       convert(binary(10),'0x' + '<value-from-state-cs>', 1))  
               set @end_lsn =   
                       convert(binary(10),'0x' + '<value-from-state-ce>', 1)  
               select * from cdc.fn_cdc_get_net_changes_dbo_Table1(@start_lsn,  
@end_lsn, '<mode>')  
```  
  
 其中：  
  
-   \<cdc-enabled-database-name>這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含變更資料表的資料庫名稱。  
  
-   \<value-from-state-cs>這是 CDC 狀態變數中顯示為 CS/ \<value-from-state-cs> /（cs 代表目前處理範圍開始）的值。  
  
-   \<value-from-state-ce>這是 CDC 狀態變數中顯示為 CE/ \<value-from-state-cs> /（ce 代表目前處理範圍結束）的值。  
  
-   \<mode>這是 CDC 處理模式。 處理模式有下列其中一個值：[全部]  、[全部 (含舊值)]  、[淨]  、[淨 (含更新遮罩)]  、[淨 (含合併)]  。  
  
 此指令碼會在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中重現問題，協助您輕鬆重現及識別錯誤以隔離問題。  
  
#### <a name="sql-server-error-message"></a>SQL Server 錯誤訊息  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可能會傳回下列訊息：  
  
 **為程式或函數 cdc 提供的引數數目不足。 fn_cdc_get_net_changes_ \<..> 。**  
  
 此錯誤並不表示缺少引數。 它表示 CDC 狀態變數中的開始或結束 LSN 值無效。  
  
## <a name="configuring-the-cdc-source"></a>設定 CDC 來源  
 您可以透過程式設計方式或 SSIS 設計師來設定 CDC 來源。  
  
 如需詳細資訊，請參閱下列其中一個主題：  
  
-   [CDC 來源編輯器 &#40;連線管理員頁面&#41;](../cdc-source-editor-connection-manager-page.md)  
  
-   [CDC 來源編輯器 &#40;資料行頁面&#41;](../cdc-source-editor-columns-page.md)  
  
-   [CDC 來源編輯器 &#40;錯誤輸出頁面&#41;](../cdc-source-editor-error-output-page.md)  
  
 **[進階編輯器]** 對話方塊包含可以程式設計方式設定的屬性。  
  
 若要開啟 **[進階編輯器]** 對話方塊：  
  
-   在 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 專案的 [資料流程]  畫面中，以滑鼠右鍵按一下 CDC 來源，然後選取 [顯示進階編輯器]  。  
  
 如需可在 [進階編輯器]  對話方塊中設定之屬性的詳細資訊，請參閱 [CDC 來源自訂屬性](cdc-source-custom-properties.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [CDC 來源編輯器 &#40;連線管理員頁面&#41;](../cdc-source-editor-connection-manager-page.md)  
  
-   [CDC 來源編輯器 &#40;資料行頁面&#41;](../cdc-source-editor-columns-page.md)  
  
-   [CDC 來源編輯器 &#40;錯誤輸出頁面&#41;](../cdc-source-editor-error-output-page.md)  
  
-   [CDC 來源自訂屬性](cdc-source-custom-properties.md)  
  
-   [使用 CDC 來源擷取變更資料](cdc-source.md)  
  
## <a name="related-content"></a>相關內容  
  
-   mattmasson.com 上的部落格文章： [Processing Modes for the CDC Source](https://www.mattmasson.com/2012/01/processing-modes-for-the-cdc-source/)。  
  
  

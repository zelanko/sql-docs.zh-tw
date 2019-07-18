---
title: Excel 來源編輯器 （連線管理員頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelsourceadapter.connection.f1
helpviewer_keywords:
- Excel Source Editor
ms.assetid: 428e04e0-ad98-45d0-8345-12ec1b67b2eb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c3132bd65bb6f3092cc950758d4f346b5c4cd8fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059172"
---
# <a name="excel-source-editor-connection-manager-page"></a>Excel 來源編輯器 (連接管理員頁面)
  使用 **[Excel 來源編輯器]** 對話方塊的 **[連接管理員]** 節點，以選取來源要使用的 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 活頁簿。 Excel 來源會從工作表或現有活頁簿的具名範圍中讀取資料。  
  
> [!NOTE]  
>  `CommandTimeout` Excel 來源的屬性不適用於**Excel 來源編輯器**，但可以透過設定**進階編輯器**。 如需有關這個屬性的詳細資訊，請參閱＜ [Excel Custom Properties](data-flow/excel-custom-properties.md)＞的＜Excel 來源＞一節。  
  
 若要深入了解 Excel 來源，請參閱＜ [Excel Source](data-flow/excel-source.md)＞。  
  
## <a name="static-options"></a>靜態選項  
 **[無快取]**  
 從清單中選取現有的 Excel 連線管理員，或按一下 [新增]  建立新的連線管理員。  
  
 **新增**  
 使用 [Excel 連線管理員]  對話方塊來建立新的連線管理員。  
  
 **資料存取模式**  
 從來源中指定選取資料的方法。  
  
|值|描述|  
|-----------|-----------------|  
|資料表或檢視|從工作表或 Excel 檔案的具名範圍中擷取資料。|  
|資料表名稱或檢視名稱變數|在變數中指定工作表或範圍名稱。<br /><br /> **相關資訊：** [在套件中使用變數](../../2014/integration-services/use-variables-in-packages.md)|  
|SQL (命令)|使用 SQL 查詢從 Excel 檔案中擷取資料。 如需有關查詢語法的詳細資訊，請參閱＜ [Excel Source](data-flow/excel-source.md)＞。|  
|來自變數的 SQL 命令|在變數中指定 SQL 查詢文字。|  
  
 **預覽**  
 使用 [資料檢視]  對話方塊來預覽結果。 預覽最多可顯示 200 個資料列。  
  
## <a name="data-access-mode-dynamic-options"></a>資料存取模式動態選項  
  
### <a name="data-access-mode--table-or-view"></a>資料存取模式 = 資料表或檢視  
 **Excel 工作表的名稱**  
 從 Excel 活頁簿的可用工作表或具名範圍清單中，選取工作表或具名範圍的名稱。  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>資料存取模式 = 資料表名稱或檢視名稱變數  
 **變數名稱**  
 選取包含工作表名稱或具名範圍的變數。  
  
### <a name="data-access-mode--sql-command"></a>資料存取模式 = SQL 命令  
 **SQL 命令文字**  
 輸入 SQL 查詢的文字，按一下 [建立查詢]  建立查詢，或按一下 [瀏覽]  瀏覽至包含查詢文字的檔案。  
  
 **參數**  
 如果您所輸入的參數化查詢使用 ? 做為查詢文字中的參數預留位置，請使用 **[設定查詢參數]** 對話方塊，將查詢輸入參數對應到封裝變數。  
  
 **建立查詢**  
 使用 [查詢產生器]  對話方塊，以視覺化的方式來建構 SQL 查詢。  
  
 **瀏覽**  
 使用 [開啟]  對話方塊來找出包含 SQL 查詢文字的檔案。  
  
 **剖析查詢**  
 請確認查詢文字的語法。  
  
### <a name="data-access-mode--sql-command-from-variable"></a>資料存取模式 = 來自變數的 SQL 命令  
 **變數名稱**  
 選取包含 SQL 查詢文字的變數。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Excel 來源編輯器 &#40;資料行頁面&#41;](../../2014/integration-services/excel-source-editor-columns-page.md)   
 [Excel 來源編輯器 &#40;錯誤輸出頁面&#41;](../../2014/integration-services/excel-source-editor-error-output-page.md)   
 [Excel 連線管理員](connection-manager/excel-connection-manager.md)   
 [使用 Foreach 迴圈容器來執行 Excel 檔案和資料表迴圈](control-flow/foreach-loop-container.md)  
  
  

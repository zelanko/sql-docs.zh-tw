---
title: ODBC 來源編輯器（連線管理員頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.connection.f1
ms.assetid: e2c8dc83-6394-4d6c-9232-97e94be72431
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a9c4049681e671993f48594eb7ac18bad403e3e2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965008"
---
# <a name="odbc-source-editor-connection-manager-page"></a>ODBC 來源編輯器 (連接管理員頁面)
  使用 **[ODBC 來源編輯器]** 對話方塊的 **[連接管理員]** 頁面，即可選取來源的 ODBC 連接管理員。 這個頁面也可以讓您從資料庫中選取資料表或檢視。  
  
 如需有關 ODBC 來源的詳細資訊，請參閱＜ [ODBC Source](data-flow/odbc-source.md)＞。  
  
## <a name="task-list"></a>工作清單  
 **若要開啟 ODBC 來源編輯器的連接管理員頁面**  
  
-   在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，開啟具有 ODBC 來源的 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 封裝。  
  
-   在 [資料流程]**** 索引標籤上，按兩下 ODBC 來源。  
  
## <a name="options"></a>選項。  
  
### <a name="connection-manager"></a>[ODBC 來源編輯器]  
 從清單中選取現有的 ODBC 連接管理員，或按一下 [**新增**] 以建立新的連接。 此連接可以指向任何 ODBC 支援的資料庫。  
  
### <a name="new"></a>新增  
 按一下 **[新增]** 。 **[設定 ODBC 連接管理員編輯器]** 對話方塊隨即開啟，讓您能夠建立新的 ODBC 連接管理員。  
  
### <a name="data-access-mode"></a>資料存取模式  
 選取從來源中選取資料的方法。 下表將顯示這些選項：  
  
|選項|描述|  
|------------|-----------------|  
|資料表名稱|從 ODBC 資料來源中的資料表或檢視表擷取資料。 當您選取此選項時，請從清單中選取下列項目的值：|  
||**資料表或檢視表的名稱**：從清單中選取可用的資料表或檢視表，或是輸入可識別資料表的規則運算式。|  
||此清單只包含前 1000 個資料表。 如果您的資料庫包含超過 1000 個資料表，您可以輸入資料表名稱的開頭或使用 (*) 萬用字元來輸入名稱的任何部分，以便顯示您想要使用的資料表。|  
|SQL (命令)|使用 SQL 查詢從 ODBC 資料來源中擷取資料。 您應該以目前所使用之來源資料庫的語法撰寫查詢。 當您選取此選項時，請用下列其中一種方式輸入查詢：|  
||在 **[SQL 命令文字]** 欄位中輸入 SQL 查詢的文字。|  
||按一下 **[瀏覽]** ，從文字檔載入 SQL 查詢。|  
||按一下 **[剖析查詢]** 驗證查詢文字的語法。|  
  
### <a name="preview"></a>預覽  
 按一下 **[預覽]** ，最多可檢視從所選取之資料表或檢視表中擷取的前 200 個資料列。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 來源自訂屬性](data-flow/odbc-source-custom-properties.md)   
 [ODBC 來源編輯器 &#40;資料行] 頁面&#41;](../../2014/integration-services/odbc-source-editor-columns-page.md)   
 [ODBC 來源編輯器 &#40;錯誤輸出頁面&#41;](../../2014/integration-services/odbc-source-editor-error-output-page.md)  
  
  

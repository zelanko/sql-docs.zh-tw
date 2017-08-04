---
title: "ODBC 目的地編輯器 （連接管理員頁面） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.odbcdest.connection.f1
ms.assetid: f6d9c6c2-e4c4-468b-9e0d-af7b9609614d
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0f2e090b24ea11734f758033f7137523c9f2036b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="odbc-destination-editor-connection-manager-page"></a>ODBC 目的地編輯器 (連接管理員頁面)
  使用 **[ODBC 目的地編輯器]** 對話方塊的 **[連接管理員]** 頁面，即可選取目的地的 ODBC 連接管理員。 這個頁面也可以讓您從資料庫中選取資料表或檢視表。  
  
 如需有關 ODBC 目的地的詳細資訊，請參閱＜ [ODBC Destination](../../integration-services/data-flow/odbc-destination.md)＞。  
  
 **若要開啟 ODBC 目的地編輯器的連接管理員頁面**  
  
## <a name="task-list"></a>工作清單  
  
-   在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟具有 ODBC 目的地的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 封裝。  
  
-   在 [資料流程] 索引標籤中，按兩下 ODBC 目的地。  
  
-   在 **[ODBC 目的地編輯器]**中，按一下 **[連接管理員]**。  
  
## <a name="options"></a>選項。  
  
### <a name="connection-manager"></a>[ODBC 目的地編輯器]  
 從清單中選取現有的 ODBC 連接管理員，或按一下 [新增] 建立新的連接。 此連接可以指向任何 ODBC 支援的資料庫。  
  
### <a name="new"></a>新增  
 按一下 **[新增]**。 **[設定 ODBC 連接管理員編輯器]** 對話方塊隨即開啟，讓您能夠建立新的連接管理員。  
  
### <a name="data-access-mode"></a>資料存取模式  
 選取將資料載入目的地的方法。 下表將顯示這些選項：  
  
|選項|說明|  
|------------|-----------------|  
|資料表名稱 - 批次|若要將 ODBC 目的地設定成以批次模式運作，請選取此選項。 當您選取此選項時，可以使用下列選項：|  
||**資料表或檢視的名稱**：從清單中選取可用的資料表或檢視表。<br /><br /> 此清單只包含前 1000 個資料表。 如果您的資料庫包含超過 1000 個資料表，您可以輸入資料表名稱的開頭或使用 (\*) 萬用字元來輸入名稱的任何部分，以便顯示您想要使用的資料表。<br /><br /> **批次大小**：輸入大量載入的批次大小。 這是當做批次載入的資料列數目。|  
|資料表名稱 - 逐列|若要將 ODBC 目的地設定成插入每個資料列至目的地資料表 (一次一個)，請選取此選項。 當您選取此選項時，可以使用下列選項：|  
||**資料表或檢視的名稱**：從清單的資料庫中選取可用的資料表或檢視表。<br /><br /> 此清單只包含前 1000 個資料表。 如果您的資料庫包含超過 1000 個資料表，您可以輸入資料表名稱的開頭或使用 (*) 萬用字元來輸入名稱的任何部分，以便顯示您想要使用的資料表。|  
  
### <a name="preview"></a>預覽  
 按一下 **[預覽]** ，最多可檢視您所選取之資料表的 200 個資料列。  
  
## <a name="see-also"></a>請參閱＜  
 [ODBC 目的地自訂屬性](../../integration-services/data-flow/odbc-destination-custom-properties.md)   
 [ODBC 目的地編輯器 &#40;[對應] 頁面 &#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)   
 [ODBC 目的地編輯器 &#40;錯誤輸出頁面 &#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
  

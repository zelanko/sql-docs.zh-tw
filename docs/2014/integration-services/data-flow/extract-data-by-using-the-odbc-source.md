---
title: 使用 ODBC 來源擷取資料 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 10f25703-49a2-4d45-abab-6b4da2a57ba5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a51457b748569f5f36e6606dc89b7f276cddd94
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437755"
---
# <a name="extract-data-by-using-the-odbc-source"></a>使用 ODBC 來源來擷取資料
  此程序描述如何使用 ODBC 來源擷取資料。 若要加入和設定 ODBC 來源，封裝必須至少含有一個「資料流程」工作。  
  
### <a name="to-extract-data-using-an-odbc-source"></a>使用 ODBC 來源擷取資料  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟所要的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 封裝。  
  
2.  按一下 **[資料流程]** 索引標籤，然後將 ODBC 來源從 **[工具箱]** 拖曳至設計介面。  
  
3.  按兩下 ODBC 來源。  
  
4.  在 **[ODBC 來源編輯器]** 對話方塊中的 **[連接管理員]** 頁面上，選取現有的 ODBC 連接管理員，或按一下 **[新增]** 以建立新的連接管理員。  
  
5.  選取資料存取方法。  
  
    -   **資料表名稱**：選取 ODBC 連接管理員連接之資料庫中的資料表或檢視，或輸入規則運算式以識別資料表。  
  
         此清單只包含前 1000 個資料表。 如果您的資料庫包含超過 1000 個資料表，您可以輸入資料表名稱的開頭或使用 (*) 萬用字元來輸入名稱的任何部分，以便顯示您想要使用的資料表。  
  
    -   **SQL 命令**：輸入 SQL 命令，或按一下 **[瀏覽]** 從文字檔載入 SQL 查詢。  
  
6.  您可以按一下 **[預覽]** ，以檢視 ODBC 來源擷取的最多 200 個資料列。  
  
7.  若要更新外部及輸出資料行之間的對應，請按一下 **[資料行]** ，並在 **[外部資料行]** 清單中選取不同的資料行。  
  
8.  如有需要，藉由編輯 **[輸出資料行]** 清單中的值，更新輸出資料行的名稱。  
  
9. 若要設定錯誤輸出，請按一下 **[錯誤輸出]** 。  
  
10. 按一下 [確定]  。  
  
11. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 來源編輯器 &#40;連線管理員頁面&#41;](../odbc-source-editor-connection-manager-page.md)   
 [ODBC 來源編輯器 &#40;資料行頁面&#41;](../odbc-source-editor-columns-page.md)   
 [ODBC 來源編輯器 &#40;錯誤輸出頁面&#41;](../odbc-source-editor-error-output-page.md)  
  
  

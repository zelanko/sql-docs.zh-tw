---
title: "使用 ODBC 目的地載入資料 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 339ec0a8-922e-48c0-97b3-fc5ee34f95e3
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 668cf193758a8dfaba90e598ccbdb7d0d84351fc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="load-data-by-using-the-odbc-destination"></a>使用 ODBC 目的地來載入資料
  此程序說明如何透過使用 ODBC 目的地載入資料。 若要加入及設定 ODBC 目的地，封裝必須已包括至少一個「資料流程」工作與來源。  
  
### <a name="to-load-data-using-an-odbc-destination"></a>使用 ODBC 目的地載入資料  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟所要的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  按一下 **[資料流程]** 索引標籤，然後將 ODBC 目的地從 **[工具箱]**拖曳到設計介面。  
  
3.  將某個資料流程元件的可用輸出拖曳到 ODBC 目的地的輸入。  
  
4.  按兩下 ODBC 目的地。  
  
5.  在 **[ODBC 目的地編輯器]** 對話方塊中的 **[連接管理員]** 頁面上，選取現有的 ODBC 連接管理員，或按一下 **[新增]** 以建立新的連接管理員。  
  
6.  選取資料存取方法。  
  
    -   **資料表名稱 - 批次**：若要將 ODBC 目的地設定成以批次模式運作，請選取此選項。 當您選取此選項時，可以設定 **[批次大小]**。  
  
    -   **資料表名稱 - 逐列**：若要將 ODBC 目的地設定成插入每個資料列至目的地資料表 (一次一個)，請選取此選項。 當您選取此選項時，資料會以一次一個資料列的方式載入到資料表。  
  
7.  在 **[資料表或檢視表的名稱]** 欄位中，從清單中選取資料庫中可用的資料表或檢視表，或是輸入可識別資料表的規則運算式。此清單只包含前 1000 個資料表。 如果您的資料庫包含超過 1000 個資料表，您可以輸入資料表名稱的開頭或使用 (*) 萬用字元來輸入名稱的任何部分，以便顯示您想要使用的資料表。  
  
8.  您可以按一下 **[預覽]** ，最多可檢視從 ODBC 目的地中選取之資料表的 200 個資料列。  
  
9. 按一下 **[對應]** ，然後將資料行從一個清單拖曳至另一個清單，使 **[可用的輸入資料行]** 清單中的資料行對應至 **[可用的目的地資料行]** 清單中的資料行。  
  
10. 若要設定錯誤輸出，請按一下 **[錯誤輸出]**。  
  
11. 按一下 **[確定]**。  
  
12. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 目的地編輯器 &#40;連接管理員頁面&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)   
 [ODBC 目的地編輯器 &#40;[對應] 頁面 &#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)   
 [ODBC 來源編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
  


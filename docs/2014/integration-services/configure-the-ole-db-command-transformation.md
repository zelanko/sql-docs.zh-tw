---
title: 設定 OLE DB 命令轉換 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- parameters [Integration Services]
- OLE DB Command transformation
ms.assetid: c800f167-3d2e-4c10-8ba3-a02f1872ccea
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8f6f14d93e840b9a206e0b5261eb9efade0f0e28
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921504"
---
# <a name="configure-the-ole-db-command-transformation"></a>設定 OLE DB 命令轉換
  若要加入及設定「OLE DB 命令」轉換，封裝必須至少已包含一個「資料流程」工作和一個來源 (例如「一般檔案」來源或 OLE DB 來源)。 此轉換通常用於執行參數化查詢。  
  
### <a name="to-configure-the-ole-db-command-transformation"></a>設定 OLE DB 命令轉換  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[資料流程]** 索引標籤，然後將「OLE DB 命令」轉換從 **[工具箱]** 拖曳至設計介面。  
  
4.  將連接子 (綠色或紅色的箭頭) 從資料來源或前一個轉換拖曳至「OLE DB 命令」轉換，將「OLE DB 命令」轉換連線到資料流程。  
  
5.  以滑鼠右鍵按一下元件，選取 [編輯] 或顯示 [進階編輯器]****。  
  
6.  在 **[連接管理員]** 索引標籤上，選取 **[連接管理員]** 清單中的 OLE DB 連接管理員。 如需相關資訊，請參閱 [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md)。  
  
7.  按一下 [元件屬性]**** 索引標籤，然後按一下 [SqlCommand]**** 方塊中的省略符號按鈕 **(...)**。  
  
8.  在 [字串值編輯器]**** 中，輸入參數化 SQL 陳述式，並使用問號 (?) 作為每個參數的參數標記。  
  
9. 按一下 [重新整理]****。 當您按一下 [重新整理]**** 時，轉換會在「外部資料行」集合中為每個參數建立資料行，並設定 DBParamInfoFlags 屬性。  
  
10. 按一下 **[輸入與輸出屬性]** 索引標籤。  
  
11. 展開 **[OLE DB 命令輸入]**，然後展開 **[外部資料行]**。  
  
12. 請確認 **[外部資料行]** 會列出 SQL 陳述式中每個參數的資料行。 資料行的名稱為 **Param_0**、 **Param_1**等。  
  
     請不要變更這些資料行名稱。 如果您變更了這些資料行名稱， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 就會針對 OLE DB 命令轉換產生驗證錯誤。  
  
     此外，請不要變更資料類型。 每個資料行的 DataType 屬性都會設定為正確的資料類型。  
  
13. 如果 **[外部資料行]** 沒有列出資料行，則您必須手動將其加入。  
  
    -   針對 SQL 陳述式中的每個參數，一次按一下 **[加入資料行]** 。  
  
    -   將資料行的名稱更新為 **Param_0**、 **Param_1**等。  
  
    -   指定 DBParamInfoFlags 屬性中的值。 該值必須與 OLE DB DBPARAMFLAGSENUM 列舉中的值相符。 如需詳細資訊，請參閱 OLE DB 參考文件集。  
  
    -   指定資料行的資料類型，並依據該資料類型指定資料行的字碼頁、長度、有效位數和小數位數。  
  
    -   若要刪除不使用的參數，請選取 **[外部資料行]** 中的參數，然後按一下 **[移除資料行]**。  
  
    -   按一下 **[資料行對應]** ，然後將 **[可用的輸入資料行]** 清單中的資料行對應至 **[可用的目的地資料行]** 清單中的參數。  
  
14. 按一下 [確定]。  
  
15. 若要儲存更新的封裝，請按一下 **[檔案]** 功能表上的 **[儲存]** 。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB 命令轉換](data-flow/transformations/ole-db-command-transformation.md)   
 [Integration Services 轉換](data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路徑](data-flow/integration-services-paths.md)   
 [資料流程工作](control-flow/data-flow-task.md)  
  
  

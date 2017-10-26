---
title: "OLE DB 命令轉換 |Microsoft 文件"
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
- sql13.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
caps.latest.revision: 55
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: 99d34e8dd153c5ca1793d14cc9638aab6529a643
ms.contentlocale: zh-tw
ms.lasthandoff: 08/19/2017

---
# <a name="ole-db-command-transformation"></a>OLE DB 命令轉換
  OLE DB 命令轉換為資料流程中每個資料列執行 SQL 陳述式。 例如，可以執行在資料庫資料表中插入、更新或刪除資料列的 SQL 陳述式。  
  
 您可以利用下列方式設定 OLE DB 命令轉換：  
  
-   提供轉換為每個資料列執行的 SQL 陳述式。  
  
-   指定 SQL 陳述式逾時之前的秒數。  
  
-   指定預設字碼頁。  
  
 SQL 陳述式通常包含參數。 參數值儲存在轉換輸入的外部資料行內，且將輸入資料行對應到外部資料行會將其同時對應到參數。 例如，若要利用資料列在 **ProductKey** 資料行中的值找到 **DimProduct** 資料表中的資料列，然後予以刪除，您可以將名為 **Param_0** 的外部資料行對應到名為 **ProductKey** 的輸入資料行，然後執行 SQL 陳述式 `DELETE FROM DimProduct WHERE ProductKey = ?`。 OLE DB 命令轉換提供了參數名稱，您無法對它們進行修改。 這些參數名稱為 **Param_0**、**Param_1** 等。  
  
 如果您使用 [進階編輯器] 對話方塊設定 OLE DB 命令轉換，SQL 陳述式中的參數可自動對應到轉換輸入的外部資料行上，按一下 [重新整理] 按鈕可以定義每個參數的特性。 但是，如果 OLE DB 命令轉換使用的 OLE DB 提供者不支援從參數中衍生參數資訊，您必須手動設定外部資料行。 這表示您必須將每個參數的資料行加入轉換的外部輸入，更新資料行名稱以使用類似 **Param_0**的名稱，指定 DBParamInfoFlags 屬性的值，並將包含參數值的輸入資料行對應到外部資料行。  
  
 DBParamInfoFlags 的值代表參數的特性。 例如，值 **1** 指定參數為輸入參數，值 **65** 指定參數為可以包含 Null 值的輸入參數。 該值必須與 OLE DB DBPARAMFLAGSENUM 列舉中的值相符。 如需詳細資訊，請參閱 OLE DB 參考文件集。  
  
 OLE DB 命令轉換包括 **SQLCommand** 自訂屬性。 屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../../../integration-services/expressions/use-property-expressions-in-packages.md)和[轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
 這個轉換有一個輸入、一個規則輸出及一個錯誤輸出。  
  
## <a name="logging"></a>記錄  
 您可以記錄 OLE DB 命令轉換對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，疑難排解 OLE DB 命令轉換對外部資料來源執行的連接和命令。 若要記錄 OLE DB 命令轉換對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷] 事件。 如需詳細資訊，請參閱[封裝執行的疑難排解工具](../../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="related-tasks"></a>相關工作  
 您可以使用 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或物件模型來設定轉換。 如需有關以程式設計方式來設定此轉換的詳細資訊，請參閱《開發人員指南》。  
  
## <a name="configure-the-ole-db-command-transformation"></a>設定 OLE DB 命令轉換
  若要加入及設定「OLE DB 命令」轉換，封裝必須至少已包含一個「資料流程」工作和一個來源 (例如「一般檔案」來源或 OLE DB 來源)。 此轉換通常用於執行參數化查詢。  
  
#### <a name="to-configure-the-ole-db-command-transformation"></a>設定 OLE DB 命令轉換  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[資料流程]** 索引標籤，然後將「OLE DB 命令」轉換從 **[工具箱]**拖曳至設計介面。  
  
4.  將連接子 (綠色或紅色的箭頭) 從資料來源或前一個轉換拖曳至「OLE DB 命令」轉換，將「OLE DB 命令」轉換連接到資料流程。  
  
5.  以滑鼠右鍵按一下元件，選取 [編輯] 或顯示 [進階編輯器]。  
  
6.  在 **[連接管理員]** 索引標籤上，選取 **[連接管理員]** 清單中的 OLE DB 連接管理員。 如需相關資訊，請參閱 [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
7.  按一下 [元件屬性] 索引標籤，然後按一下 [SqlCommand] 方塊中的刪節號按鈕 [...]。  
  
8.  在 [字串值編輯器] 中，輸入參數化 SQL 陳述式，並使用問號 (?) 作為每個參數的參數標記。  
  
9. 按一下 **[重新整理]**。 當您按一下 [重新整理] 時，轉換會在「外部資料行」集合中為每個參數建立資料行，並設定 DBParamInfoFlags 屬性。  
  
10. 按一下 **[輸入與輸出屬性]** 索引標籤。  
  
11. 展開 **[OLE DB 命令輸入]**，然後展開 **[外部資料行]**。  
  
12. 請確認 **[外部資料行]** 會列出 SQL 陳述式中每個參數的資料行。 資料行的名稱為 **Param_0**、 **Param_1**等。  
  
     請不要變更這些資料行名稱。 如果您變更了這些資料行名稱， [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 就會針對 OLE DB 命令轉換產生驗證錯誤。  
  
     此外，請不要變更資料類型。 每個資料行的 DataType 屬性都會設定為正確的資料類型。  
  
13. 如果 **[外部資料行]** 沒有列出資料行，則您必須手動將其加入。  
  
    -   針對 SQL 陳述式中的每個參數，一次按一下 **[加入資料行]** 。  
  
    -   將資料行的名稱更新為 **Param_0**、 **Param_1**等。  
  
    -   指定 DBParamInfoFlags 屬性中的值。 該值必須與 OLE DB DBPARAMFLAGSENUM 列舉中的值相符。 如需詳細資訊，請參閱 OLE DB 參考文件集。  
  
    -   指定資料行的資料類型，並依據該資料類型指定資料行的字碼頁、長度、有效位數和小數位數。  
  
    -   若要刪除不使用的參數，請選取 **[外部資料行]**中的參數，然後按一下 **[移除資料行]**。  
  
    -   按一下 **[資料行對應]** ，然後將 **[可用的輸入資料行]** 清單中的資料行對應至 **[可用的目的地資料行]** 清單中的參數。  
  
14. 按一下 **[確定]**。  
  
15. 若要儲存更新的封裝，請按一下 **[檔案]** 功能表上的 **[儲存]** 。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  


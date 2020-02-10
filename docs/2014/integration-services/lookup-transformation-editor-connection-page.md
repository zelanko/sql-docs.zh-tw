---
title: 查閱轉換編輯器（連接頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.referencetable.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: e90d6b69-5a26-43c5-8433-5c3c9588e08c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7985f713093e839d258a0c9b80bb5d4e6e58f37f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66057946"
---
# <a name="lookup-transformation-editor-connection-page"></a>查閱轉換編輯器 (連接頁面)
  使用 **[查閱轉換編輯器]** 對話方塊的 **[連接]** 頁面，來選取連接管理員。 如果您選取 OLE DB 連接管理員，也可以選取查詢、資料表或檢視來產生參考資料集。  
  
 若要深入了解查閱轉換，請參閱＜ [Lookup Transformation](data-flow/transformations/lookup-transformation.md)＞。  
  
## <a name="options"></a>選項。  
 當您在 **[查閱轉換編輯器]** 對話方塊的 [一般] 頁面上選取 **[完整快取]** 和 **[快取連接管理員]** 時，可使用下列選項：  
  
 **快取連線管理員**  
 從清單中選取現有的快取連線管理員，或按一下 [新增]**** 來建立新的連線。  
  
 **新增**  
 使用 [快取連線管理員編輯器]**** 對話方塊來建立新的連線。  
  
 當您在 **[查閱轉換編輯器]** 對話方塊的 [一般] 頁面上選取 **[完整快取]**、 **[部分快取]** 或 **[無快取]** 以及 **[OLE DB 連接管理員]** 時，可以使用下列選項。  
  
 **OLE DB 連線管理員**  
 從清單中選取現有的 OLE DB 連線管理員，或按一下 [新增]**** 來建立新連線。  
  
 **新增**  
 使用 [設定 OLE DB 連接管理員]**** 對話方塊來建立新的連接。  
  
 **使用資料表或視圖**  
 從清單中選取現有的資料表或檢視，或按一下 [新增]**** 來建立新的資料表。  
  
> [!NOTE]  
>  如果在 **[查閱轉換編輯器]** 的 **[進階]** 頁面上指定 SQL 陳述式，則該 SQL 陳述式會覆寫並取代此處所選取的資料表名稱。 如需詳細資訊，請參閱 [查閱轉換編輯器 &#40;進階頁面&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)＞。  
  
 **新增**  
 使用 [建立資料表]**** 對話方塊建立新的資料表。  
  
 **使用 SQL 查詢的結果**  
 選擇此選項以瀏覽至預先存在的查詢、建立新查詢、檢查查詢語法，以及預覽查詢結果。  
  
 **建立查詢**  
 使用 [查詢產生器]**** (用來以瀏覽資料的方式建立查詢的圖形化工具)，來建立要執行的 Transact-SQL 陳述式。  
  
 **瀏覽**  
 使用此選項即可瀏覽至預先存在且已儲存為檔案的查詢。  
  
 **剖析查詢**  
 檢查查詢的語法。  
  
 **預覽**  
 使用 [預覽查詢結果]**** 對話方塊來預覽結果。 此選項最多可顯示 200 個資料列。  
  
## <a name="external-resources"></a>外部資源  
 blogs.msdn.com 上的部落格文章： [查閱快取模式](https://go.microsoft.com/fwlink/?LinkId=219518)  
  
## <a name="see-also"></a>另請參閱  
 [查閱轉換編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)   
 [查閱轉換編輯器 &#40;資料行頁面&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [查閱轉換編輯器 &#40;Advanced Page&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [查閱轉換編輯器 &#40;錯誤輸出頁面&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [模糊查閱轉換](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  

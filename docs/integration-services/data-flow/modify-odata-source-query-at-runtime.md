---
title: "在執行階段提供 OData 來源查詢 | Microsoft Docs"
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
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 457e4f5b8d52be56aa82f854e5a87caae72ebd99
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="provide-an-odata-source-query-at-runtime"></a>在執行階段提供 OData 來源查詢
 您可以在執行階段修改 OData 來源查詢，修改的方式是將「運算式」加入資料流程工作的 **[OData Source].[Query]** 屬性。  
  
 傳回的資料行必須是設計階段所傳回的相同資料行，否則會在執行封裝時收到錯誤。 在使用 $select 查詢選項時，請務必指定相同的資料行 (以相同順序)。 使用 $select 選項有一個更安全的替代方法，也就是直接從來源元件 UI 取消選取您不想要的資料行。  
  
 有幾個不同的方式可以在執行階段動態設定查詢值。 以下是一些較為常見的方法。  
  
## <a name="provide-the-query-as-a-parameter"></a>以參數形式提供查詢  
 下列程序示範如何將 OData 來源元件所使用的查詢公開為封裝的參數。  
  
1.  以滑鼠右鍵按一下 [資料流程工作]，然後選取 [參數化…] 選項。  
  
2.  在 [參數化] 對話方塊中，針對 [屬性] 選取 **[\<OData 來源元件的名稱>].[Query]**。  
  
3.  選擇是要 [建立新的參數] 還是 [使用現有的參數]。  
  
4.  如果您選取 [建立新的參數]：  
  
    1.  輸入參數的 [名稱] 和 [描述]。  
  
    2.  指定參數的預設 [值]。  
  
    3.  為參數指定 [範圍] ([封裝] 或 [專案])。  
  
    4.  指定參數是否為 [必要]  
  
5.  按一下 **[確定]** ，關閉對話方塊。  
  
## <a name="provide-the-query-with-an-expression"></a>以運算式提供查詢
 當您想要在執行階段以動態方式建構查詢字串時，此方法相當實用。
  
1.  選取包含您的 [OData 來源] 的 [資料流程工作]。  
  
2.  在 [屬性] 視窗中，反白顯示 [運算式] 屬性。  
  
3.  按一下 … (省略符號) 按鈕，即可開啟 [屬性運算式編輯器]。  
  
4.  選取 **[OData Source].[Query]** 屬性。  
  
5.  按一下 … (省略符號) 按鈕 (針對 [運算式])。  
  
6.  輸入 [運算式]。  
  
7.  按一下 [確定] 。  
  
> [!NOTE]  
> 當您使用這種方法時，您必須確定設定的值具有正確的 URL 編碼。 當從使用者輸入接受值時 (例如，從參數設定個別查詢選項值)，您必須確定這些值已經過驗證，以免可能發生 SQL 資料隱碼類型的攻擊。  
  
  

---
title: "提供在執行階段的 OData 來源查詢 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 9da1f1be0a790d01f9403d6fc05a5c1498c0ee8b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/23/2017

---
# <a name="provide-an-odata-source-query-at-runtime"></a>提供在執行階段的 OData 來源查詢
 您可以透過加入修改 OData 來源查詢，在執行階段*運算式*至**[OData 來源]。 [Query]**資料流程工作的屬性。  
  
 傳回的資料行一定要在設計階段，傳回相同的資料行否則，會執行封裝時收到錯誤。 在使用 $select 查詢選項時，請務必指定相同的資料行 (以相同順序)。 使用 $select 選項有一個更安全的替代方法，也就是直接從來源元件 UI 取消選取您不想要的資料行。  
  
 有幾個不同的方式可以在執行階段動態設定查詢值。 以下是一些較為常見的方法。  
  
## <a name="provide-the-query-as-a-parameter"></a>提供做為參數的查詢  
 下列程序示範如何公開 OData 來源元件所使用的封裝參數的查詢。  
  
1.  以滑鼠右鍵按一下 [資料流程工作]，然後選取 [參數化…] 選項。  
  
2.  在**參數化**對話方塊中，選取**[\<OData 來源元件名稱 >]。 [Query]**如**屬性**。  
  
3.  選擇是要 [建立新的參數] 還是 [使用現有的參數]。  
  
4.  如果您選取**建立新的參數**:  
  
    1.  輸入參數的 [名稱] 和 [描述]。  
  
    2.  指定參數的預設 [值]。  
  
    3.  為參數指定 [範圍] ([封裝] 或 [專案])。  
  
    4.  指定參數是否為 [必要]  
  
5.  按一下 **[確定]** ，關閉對話方塊。  
  
## <a name="provide-the-query-with-an-expression"></a>提供查詢的運算式
 當您想要以動態方式建構查詢字串，在執行階段時，這個方法會很有用。
  
1.  選取**Data Flow Task** ，其中包含您**OData 來源**。  
  
2.  在 [屬性] 視窗中，反白顯示 [運算式] 屬性。  
  
3.  按一下 … （省略符號） 按鈕即可啟動**屬性運算式編輯器**。  
  
4.  選取 **[OData Source].[Query]** 屬性。  
  
5.  按一下 … （省略符號） 按鈕，**運算式**。  
  
6.  輸入 [運算式]。  
  
7.  按一下 **[確定]**。  
  
> [!NOTE]  
> 當您使用這個方法時，您必須確定您所設定的值是正確編碼的 URL。 當從使用者輸入接受值時 (例如，從參數設定個別查詢選項值)，您必須確定這些值已經過驗證，以免可能發生 SQL 資料隱碼類型的攻擊。  
  
  

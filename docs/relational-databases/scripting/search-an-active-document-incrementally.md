---
title: "以累加方式搜尋作用中的文件 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- searches [SQL Server Management Studio], incremental
- Query Editor [SQL Server Management Studio], incremental search
- incremental searches [SQL Server Management Studio]
ms.assetid: 490bb36c-dd43-4219-9e2a-ff27046b9395
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba2c50eadb3e3f8a93a4f1f24bddf7d4bc7c6637
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="search-an-active-document-incrementally"></a>以累加方式搜尋作用中的文件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 您可以輸入文字，以累加方式來搜尋單一文件或視窗。 搜尋作業會反白顯示第一組符合文件或視窗中之累加搜尋期間所輸入之字元的字元。 累加搜尋會自動搜尋文件或視窗內的所有文字，不過，隱藏的文字除外。  
  
 對於 **[大小寫須相符]** 選項，累加搜尋會使用上一次搜尋的準則。 例如，如果您利用 [檔案中尋找] 對話方塊搜尋了多個檔案，且選取 [大小寫須相符]，您下次累加搜尋時，搜尋會區分大小寫。  
  
### <a name="to-search-incrementally"></a>累加搜尋  
  
1.  開啟您要搜尋的檔案或視窗。  
  
2.  在 **[編輯]** 功能表上，指向 **[進階]**，再按一下 **[累加搜尋]**。  
  
     此時游標圖示會改成含箭頭 (表示搜尋方向) 的雙筒望遠鏡，狀態列會顯示「累加搜尋」。  
  
3.  開始輸入文字字串。  
  
     狀態列會顯示您輸入的文字，編輯器會反白顯示符合這個文字的第一個出現項目。 當您繼續輸入時，編輯器會移到下一個相符項目，並反白顯示這個項目。 如果找不到相符項目，狀態列會顯示如下：  
  
    ```  
    Incremental Search: <text> (not found)  
    ```  
  
 累加搜尋是從文件的目前位置開始執行，由上至下，由左至右。 您可以利用鍵盤快速鍵來執行累加搜尋。  
  
> [!NOTE]  
>  如需完整的鍵盤快速鍵清單，請參閱 [SQL Server Management Studio 鍵盤快速鍵](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)。  
  
## <a name="see-also"></a>另請參閱  
 [搜尋和取代](../../relational-databases/scripting/search-and-replace.md)   
 [以互動方式搜尋文件](../../relational-databases/scripting/search-documents-interactively.md)   
 [使用結果清單搜尋文件](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [使用萬用字元搜尋文字](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [使用規則運算式搜尋文字](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  

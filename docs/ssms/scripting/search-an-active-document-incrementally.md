---
title: 以累加方式搜尋作用中的文件
description: 了解如何以累加方式來搜尋單一文件或視窗。 當鍵入時，累加搜尋作業會醒目提示您在該點所鍵入內容的下一個出現項目。 系統會忽略隱藏的文字。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], incremental
- Query Editor [SQL Server Management Studio], incremental search
- incremental searches [SQL Server Management Studio]
ms.assetid: 490bb36c-dd43-4219-9e2a-ff27046b9395
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 390ffb66c98f2328b8bfb1807a1c6dc7f4a78def
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901946"
---
# <a name="search-an-active-document-incrementally"></a>以累加方式搜尋作用中的文件
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  您可以輸入文字，以累加方式來搜尋單一文件或視窗。 搜尋作業會反白顯示第一組符合文件或視窗中之累加搜尋期間所輸入之字元的字元。 累加搜尋會自動搜尋文件或視窗內的所有文字，不過，隱藏的文字除外。  
  
 對於 **[大小寫須相符]** 選項，累加搜尋會使用上一次搜尋的準則。 例如，如果您利用 [檔案中尋找]**** 對話方塊搜尋了多個檔案，且選取 [大小寫須相符]****，您下次累加搜尋時，搜尋會區分大小寫。  
  
### <a name="to-search-incrementally"></a>累加搜尋  
  
1.  開啟您要搜尋的檔案或視窗。  
  
2.  在 **[編輯]** 功能表上，指向 **[進階]** ，再按一下 **[累加搜尋]** 。  
  
     此時游標圖示會改成含箭頭 (表示搜尋方向) 的雙筒望遠鏡，狀態列會顯示「累加搜尋」。  
  
3.  開始輸入文字字串。  
  
     狀態列會顯示您輸入的文字，編輯器會反白顯示符合這個文字的第一個出現項目。 當您繼續輸入時，編輯器會移到下一個相符項目，並反白顯示這個項目。 如果找不到相符項目，狀態列會顯示如下：  
  
    ```  
    Incremental Search: <text> (not found)  
    ```  
  
 累加搜尋是從文件的目前位置開始執行，由上至下，由左至右。 您可以利用鍵盤快速鍵來執行累加搜尋。  
  
> [!NOTE]  
>  如需完整的鍵盤快速鍵清單，請參閱 [SQL Server Management Studio 鍵盤快速鍵](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)。  
  
## <a name="see-also"></a>另請參閱  
 [搜尋和取代](../../relational-databases/scripting/search-and-replace.md)   
 [以互動方式搜尋文件](../../relational-databases/scripting/search-documents-interactively.md)   
 [使用結果清單搜尋文件](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [使用萬用字元搜尋文字](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [使用規則運算式搜尋文字](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  

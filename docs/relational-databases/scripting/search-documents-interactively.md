---
title: "以互動方式搜尋文件 | Microsoft Docs"
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
- interactive searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], interactive
- Query Editor [SQL Server Management Studio], interactive search
ms.assetid: dae65ac5-67af-45c6-a6e0-952fea26d680
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b1b665a2ce68bf3c99c950d8a943052d123c2f6a
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="search-documents-interactively"></a>以互動方式搜尋文件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 您可以利用 [尋找和取代] 對話方塊，搜尋一或多個開啟的檔案或視窗，並逐一搜尋相符的項目。 這項技術可讓您在環繞相符項目的文字內容中，檢閱每項個別的搜尋相符項目。 您也可以選擇執行大量尋找作業，或利用 [尋找和取代] 對話方塊，以報表格式檢閱搜尋相符項目。  
  
### <a name="to-search-all-open-documents"></a>搜尋所有開啟的文件  
  
1.  開啟您要搜尋的項目。  
  
2.  在 [編輯] 功能表上，指向 [尋找和取代]，再按一下 [快速尋找]。  
  
3.  在 [尋找和取代] 文字方塊中，輸入要搜尋的文字。  
  
4.  在 [查詢] 清單中，選取 [所有開啟的文件]。  
  
    > [!NOTE]  
    >  當選取 [所有開啟的文件] 時，可能不會搜尋某些開啟的檔案。 搜尋只包括文字檢視 (如 [程式碼] 檢視) 所開啟的檔案。 搜尋不包括 [設計師] 檢視中的檔案。  
  
5.  選取其他搜尋選項來增加搜尋的精確度。  
  
6.  按一下 [尋找下一個] 開始搜尋，再繼續按 [尋找下一個]，直到搜尋到最後一個檔案為止。  
  
 當搜尋通過文件的開頭或結尾時，狀態列會出現一則訊息。 當搜尋到了搜尋的起點時，會出現一個訊息方塊。  
  
#### <a name="to-replace-in-all-active-files-interactively"></a>在所有作用檔案中，以互動方式取代  
  
1.  在 [編輯] 功能表上，指向 [尋找和取代]，再按一下 [快速尋找]。  
  
2.  在 [尋找目標] 方塊中，輸入要搜尋的文字。  
  
3.  在 **[取代成]** 方塊中，輸入用來取代搜尋文字的文字。  
  
4.  在 [查詢] 清單中，選取 [所有開啟的文件]。  
  
5.  按一下 [取代]，再繼續按 [取代]，直到取代最後一個檔案中最後一個相符的項目為止。 若要跳過不要取代的相符項目，請按一下 [尋找下一個]。  
  
     -或-  
  
     選擇 [取代全部] 取代所有相符項目。 此時會出現一個訊息方塊，列出取代的總數。  
  
 [取代全部] 命令會取代所有搜尋相符項目，其中包括您利用 [尋找下一個] 按鈕所略過的相符項目。 若要取消 [取代全部]，請在關閉任何檔案之前，按一下 [編輯] 功能表中的 [恢復]。  
  
## <a name="see-also"></a>另請參閱  
 [以累加方式搜尋作用中的文件](../../relational-databases/scripting/search-an-active-document-incrementally.md)   
 [搜尋和取代](../../relational-databases/scripting/search-and-replace.md)   
 [使用結果清單搜尋文件](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [使用萬用字元搜尋文字](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [使用規則運算式搜尋文字](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  

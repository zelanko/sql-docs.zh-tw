---
title: 搜尋和取代
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- match case [SQL Server]
- undo operations
- searches [SQL Server Management Studio]
- replacing text
- quick search and replaces [SQL Server Management Studio]
- Query Editor [SQL Server Management Studio], undo
- Query Editor [SQL Server Management Studio], searching
- regular expressions [SQL Server Management Studio]
- finding text [SQL Server Management Studio]
- text [SQL Server], search and replace operations
- finding [SQL Server Management Studio]
- locating text
- Query Editor [SQL Server Management Studio], replacing text
- Find and Replace dialog box
- wildcard options [SQL Server Management Studio]
- match whole word [SQL Server]
- searches [SQL Server Management Studio], replacing
ms.assetid: 3641c7b3-3e3e-4ddd-af82-c15b50004f94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 631b6864529e903516857f68ea421365c144afef
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243296"
---
# <a name="search-and-replace"></a>搜尋和取代
  您可以利用多種不同的方式來尋找和取代文字。 在 **[編輯]** 功能表上， **[尋找和取代]** 提供了四個選項： **[快速尋找]**、 **[快速取代]**、 **[檔案中尋找]** 和 **[檔案中取代]**。 這些選項會開啟各個版本的 **[尋找和取代]** 對話方塊。 您也可以不用對話方塊，而利用累加搜尋鍵盤快速鍵來搜尋。 這些技術可讓您控制尋找和取代的範圍，以及選擇檢閱搜尋相符項目和取代項目的方法。  
  
 當您搜尋和取代文字時，您應該考慮下列各點：  
  
-   
  **[尋找和取代]** 對話方塊所設定的選項會影響所有搜尋。 這些選項包括 **[大小寫須相符]**、 **[全字拼寫須相符]**、 **[向上搜尋]**、 **[搜尋隱藏文字]**、 **[萬用字元]**、 **[規則運算式]**、 **[查詢所有開啟的文件]** 和 **[查詢目前專案]**。 並非 **[尋找和取代]** 對話方塊的所有版本都提供了所有選項。  
  
-   **復原**僅適用于在取代作業之後保持開啟狀態的檔。  
  
-   跨多個檔案的 [**全部取代**] 作業的 [**復原**]，會被視為跨所有受影響檔案的單一、大量動作。 也就是說，您無法只恢復某些檔案中的變更，卻保留其他檔案中的變更。  
  
 一般而言，您無法利用圖形檢視來搜尋項目。  
  
## <a name="see-also"></a>另請參閱  
 [以累加方式搜尋使用中的檔](search-an-active-document-incrementally.md)   
 [以互動方式搜尋檔](search-documents-interactively.md)   
 [使用結果清單搜尋檔](search-documents-using-results-lists.md)   
 [使用萬用字元搜尋文字](search-text-with-wildcards.md)   
 [使用正則運算式搜尋文字](search-text-with-regular-expressions.md)  
  
  

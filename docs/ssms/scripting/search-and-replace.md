---
title: 搜尋和取代
description: 了解尋找和取代文字的四種不同方式，其中每一種都會顯示自身版本的 [尋找] 和 [取代] 對話方塊。 [尋找和取代] 選項設定會影響所有搜尋方式。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b1a75530245a3f3727fc47dee817b6a40416439
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036371"
---
# <a name="search-and-replace"></a>搜尋和取代
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  您可以利用多種不同的方式來尋找和取代文字。 在 [編輯] 功能表上，[尋找和取代] 提供四個選擇：[快速尋找]、[快速取代]、[在檔案中尋找] 或 [在檔案中取代]。 這些選項會開啟各個版本的 **[尋找和取代]** 對話方塊。 您也可以不用對話方塊，而利用累加搜尋鍵盤快速鍵來搜尋。 這些技術可讓您控制尋找和取代的範圍，以及選擇檢閱搜尋相符項目和取代項目的方法。  
  
 當您搜尋和取代文字時，您應該考慮下列各點：  
  
-   **[尋找和取代]** 對話方塊所設定的選項會影響所有搜尋。 這些選項包括 **[大小寫須相符]**、 **[全字拼寫須相符]**、 **[向上搜尋]**、 **[搜尋隱藏文字]**、 **[萬用字元]**、 **[規則運算式]**、 **[查詢所有開啟的文件]** 和 **[查詢目前專案]**。 並非 **[尋找和取代]** 對話方塊的所有版本都提供了所有選項。  
  
-   只有在取代作業之後維持開啟狀態的文件，才能夠使用 **[恢復]** 。  
  
-   跨越多個檔案的 **[全部取代]** 作業，其 **[恢復]** 會被視為跨越所有受影響之檔案的單一龐大動作。 也就是說，您無法只恢復某些檔案中的變更，卻保留其他檔案中的變更。  
  
 一般而言，您無法利用圖形檢視來搜尋項目。  
  
## <a name="see-also"></a>另請參閱  
 [以累加方式搜尋作用中的文件](./search-an-active-document-incrementally.md)   
 [以互動方式搜尋文件](./search-documents-interactively.md)   
 [使用結果清單搜尋文件](./search-documents-using-results-lists.md)   
 [使用萬用字元搜尋文字](./search-text-with-wildcards.md)   
 [使用規則運算式搜尋文字](./search-text-with-regular-expressions.md)  
  

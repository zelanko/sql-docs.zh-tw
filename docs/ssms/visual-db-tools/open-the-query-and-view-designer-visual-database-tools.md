---
title: 開啟查詢和檢視表設計工具 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- opening View Designer
- View Designer, opening
- Query Designer [SQL Server], opening
- opening Query Designer
ms.assetid: b473f258-d53c-41c0-9ad9-528a2ff141f4
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7c899f595c0c351982f7d4e0bfbf3ad52c17f0f0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33049765"
---
# <a name="open-the-query-and-view-designer-visual-database-tools"></a>開啟查詢和檢視表設計工具 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
在開啟檢視的定義、顯示查詢或檢視的結果，或者建立或開啟查詢時，[查詢和檢視設計師] 會開啟。 這包含四個個別的窗格：  
  
-   [圖表] 窗格會以圖形顯示您從資料連接所選取的資料表或資料表值物件。 同時還會顯示資料表或物件之間的任何聯結關聯性。  
  
-   只要將您的選擇輸入於類似工作表的方格，[準則] 窗格便可以讓您指定查詢選項，例如，要顯示的資料行、如何排序結果，以及要選取的資料列。  
  
-   您可以使用 [SQL] 窗格建立您自己的 SQL 陳述式，也可以使用 [準則] 窗格和 [圖表] 窗格建立陳述式。在這個情況中，SQL 陳述式會在 [SQL] 窗格中建立。 建立查詢時，[SQL] 窗格將自動更新並重新格式化以方便您讀取。  
  
-   [結果] 窗格顯示的是最近執行選取查詢的結果 (其他查詢類型的結果則顯示在訊息方塊中)。  
  
-   這些窗格可以用來使用查詢和檢視。  
  
-   開啟檢視或查詢時，某些窗格或所有窗格會一併開啟。 哪些窗格會開啟，會根據 [選項] 對話方塊中的設定以及所連接的資料庫管理系統而定。 預設值是四個窗格全部開啟。  
  
### <a name="to-open-the-query-and-view-designer-for-a-view"></a>開啟檢視的查詢和檢視設計師  
  
1.  在物件總管中，以滑鼠右鍵按一下您要開啟的檢視，然後按一下 [設計] 或 [開啟檢視]。  
  
    如果您選擇 [設計]，查詢和檢視表設計工具窗格即會依照 [選項] 對話方塊中選取的選項開啟。 如果您選擇 [開啟檢視]，只有 [結果] 窗格預設會開啟。  
  
### <a name="to-open-the-query-and-view-designer-for-an-existing-query"></a>若要開啟現有查詢的查詢和檢視設計師  
  
1.  在方案總管中，展開 [查詢] 資料夾。  
  
2.  按兩下要開啟的查詢。  
  
3.  反白顯示查詢陳述式，在反白顯示區域上按一下滑鼠右鍵，然後按一下 [在編輯器中設計查詢]。  
  
## <a name="see-also"></a>另請參閱  
[設計查詢和檢視使用說明主題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[查詢和檢視表設計工具 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)  
  

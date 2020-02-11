---
title: 解決 Excel 資料列限制 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 84f01e85a0a93ef1f2a14b2b01b4180143153865
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107545"
---
# <a name="work-around-the-excel-row-limitation"></a>解決 Excel 資料列限制
  本主題說明如何在您將報表匯出至 Excel 時解決 Excel 2003 的資料列限制。 此因應措施適用於只包含資料表的報表。  
  
 Excel 2003 在每張工作表中所支援的資料列上限為 65,536 列。 您可以在特定資料列數目之後強制使用明確分頁符號來避開這個限制。 Excel 轉譯器會針對每一個明確分頁符號建立新的工作表。  
  
### <a name="to-create-an-explicit-page-break"></a>若要建立明確分頁符號  
  
1.  在 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] 或報表管理員中開啟報表。  
  
2.  以滑鼠右鍵按一下資料表中的資料列，然後按一下 [**加入群組** > ] [**父群組**] 來加入外部資料表群組。  
  
     ![選取父群組](../media/datarow-selectparentgroup.png "選取父群組")  
  
3.  在 [群組依據]**** 運算式方塊中輸入下列公式，然後按一下 [確定]**** 來加入父群組。  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     此公式會針對資料集中的每一組 65000 個資料列指派一個數字。 為群組定義分頁符號時，這個運算式每隔 65000 個資料列就會產生一個分頁符號。  
  
     加入外部資料表群組會將群組資料行加入至報表中。  
  
4.  以滑鼠右鍵按一下群組資料行標頭來刪除群組資料行，再按一下 [刪除資料行]****，並選取 [只刪除資料行]****，然後按一下 [確定]****。  
  
     ![刪除群組資料行](../media/groupcolumn-delete-updated.png "刪除群組資料行")  
  
5.  以滑鼠右鍵按一下 [資料列群組]**** 區段中的 [群組 1]****，然後按一下 [群組屬性]****。  
  
     ![檢視群組屬性](../media/groupproperties-updated.png "檢視群組屬性")  
  
6.  在 [群組屬性]**** 對話方塊的 [排序]**** 頁面上，選取預設排序選項，然後按一下 [刪除]****。  
  
     ![刪除預設排序](../media/groupproperties-sorting-updated.png "刪除預設排序")  
  
7.  在 [分頁符號]**** 頁面上，按一下 [在群組的每個執行個體之間]****，然後按一下 [確定]****。  
  
     ![設定分頁符號](../media/groupproperties-pagebreaks-updated.png "設定分頁符號")  
  
8.  儲存報告。 當您將它匯出至 Excel 時，它會匯出到多個工作表，而且每個工作表最多包含 65000 個資料列。  
  
  

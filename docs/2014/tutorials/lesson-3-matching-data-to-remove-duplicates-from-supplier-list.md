---
title: 第3課：比對資料以從供應商清單中移除重複專案 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 059170b6-d62e-4b28-9451-99a0cc7e1f5f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c59a2fce106b08f53722ce44ae69225b680d7925
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484657"
---
# <a name="lesson-3-matching-data-to-remove-duplicates-from-supplier-list"></a>第 3 課：比對資料，以便從供應商清單中移除重複項
  您會藉由在知識庫中建立比對原則，準備知識庫來執行比對活動。 知識庫中只能有一個比對原則。 比對原則是由一個或多個比對規則所組成。 規則會識別與比對程序有關的定義域，並指定每個定義域值在比對判斷中攜帶的加權。 您會在規則中指定定義域值是否必須完全相符或者可以類似，以及相似度的程度。 您也會指定定義域比對是否為比對程序的必要條件。 您可以個別測試每個規則，並針對取樣資料測試整個原則。 測試程式會顯示比對分數大於叢集（群組）中 DQS 設定所指定之**最低記錄分數**臨界值的記錄。 您可以持續調整原則中的規則，直到滿意為止。  
  
 在定義原則之後，您會建立資料品質專案來執行比對活動。 比對專案會將比對原則中的比對規則套用到要評估的資料來源。 這個程序會評估任何兩個資料列相符的可能性。 當 DQS 執行比對分析時，它會建立 DQS 視為相符的記錄叢集。 DQS 會隨機將其中一筆記錄識別為樞紐記錄。 您可以驗證及拒絕未適當符合叢集的任何記錄。 如需詳細資訊，請參閱建立比對[原則](https://msdn.microsoft.com/library/hh270290.aspx)主題。  
  
 在這一課，您會執行比對活動，從供應商清單中移除重複項。 首先，您要建立一個比對原則，其中包含一個規則來識別供應商清單中的重複項，然後將原則發行到知識庫。 接下來，您要建立並執行資料品質專案以進行比對。 最後，您會將比對活動中的結果匯出到 Excel 檔案，您稍後會使用這個檔案將資料上傳到 Master Data Services (MDS)。  
  
## <a name="next-step"></a>後續步驟  
 [工作 1：定義比對原則](../../2014/tutorials/task-1-defining-a-matching-policy.md)  
  
  

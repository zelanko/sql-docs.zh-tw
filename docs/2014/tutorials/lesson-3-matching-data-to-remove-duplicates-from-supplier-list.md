---
title: 第 3 課： 比對資料以移除重複項從供應商清單 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 059170b6-d62e-4b28-9451-99a0cc7e1f5f
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f244dc7d62f19967aae7ee3bc32a634008fcc94e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265776"
---
# <a name="lesson-3-matching-data-to-remove-duplicates-from-supplier-list"></a>第 3 課：比對資料，以便從供應商清單中移除重複項
  您會藉由在知識庫中建立比對原則，準備知識庫來執行比對活動。 知識庫中只能有一個比對原則。 比對原則是由一個或多個比對規則所組成。 規則會識別與比對程序有關的定義域，並指定每個定義域值在比對判斷中攜帶的加權。 您會在規則中指定定義域值是否必須完全相符或者可以類似，以及相似度的程度。 您也會指定定義域比對是否為比對程序的必要條件。 您可以個別測試每個規則，並針對取樣資料測試整個原則。 測試程序會顯示的記錄比對分數會大於**最低記錄分數**DQS 組態內的叢集 （群組） 中指定的臨界值。 您可以持續調整原則中的規則，直到滿意為止。  
  
 在定義原則之後，您會建立資料品質專案來執行比對活動。 比對專案會將比對原則中的比對規則套用到要評估的資料來源。 這個程序會評估任何兩個資料列相符的可能性。 當 DQS 執行比對分析時，它會建立 DQS 視為相符的記錄叢集。 DQS 會隨機將其中一筆記錄識別為樞紐記錄。 您可以驗證及拒絕未適當符合叢集的任何記錄。 請參閱[Create a Matching Policy](http://msdn.microsoft.com/library/hh270290.aspx)如需詳細資訊。  
  
 在這一課，您會執行比對活動，從供應商清單中移除重複項。 首先，您要建立一個比對原則，其中包含一個規則來識別供應商清單中的重複項，然後將原則發行到知識庫。 接下來，您要建立並執行資料品質專案以進行比對。 最後，您會將比對活動中的結果匯出到 Excel 檔案，您稍後會使用這個檔案將資料上傳到 Master Data Services (MDS)。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 1：定義比對原則](../../2014/tutorials/task-1-defining-a-matching-policy.md)  
  
  

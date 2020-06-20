---
title: 工作5：設定以詞彙為基礎的關聯性 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 5f10c82ef5e0b63e0b81b630ed0340545c876661
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064737"
---
# <a name="task-5-setting-term-based-relationships"></a>工作 5：設定以詞彙為主的關聯
  在這項工作中，您會針對**供應商名稱**網域的值定義幾個以詞彙為主的關聯。 以詞彙為主的關聯可讓您針對屬於定義域值的詞彙進行更正。 它會啟用多個值，這些值除了被視為相同同義字的共同部分拼字以外，都是相同的。 例如， **inc.** 可以更正為已**納入**。 DQS 會在知識探索、清理或比對程序中使用這些關聯。 如需詳細資訊，請參閱[建立以詞彙為基礎](https://msdn.microsoft.com/library/hh510404.aspx)的關聯。  
  
1.  在 [**網域] 清單**中選取 [**供應商名稱**]。  
  
2.  切換至右窗格中的 [以**詞彙為基礎的關聯**性] 索引標籤。  
  
3.  按一下工具列上的 [**加入新關聯**] 按鈕，以加入資料表的關聯性。  
  
4.  針對 [**值**欄位] 和 [**公司**] 輸入 [ **Co** ] 作為 [**更正為**] 欄位。  
  
5.  針對以下的值重複上述兩個步驟：  
  
    |值|更正為|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![以詞彙為主的關聯](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "以詞彙為主的關聯")  
  
## <a name="next-step"></a>後續步驟  
 [工作 6：設定同義字](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  

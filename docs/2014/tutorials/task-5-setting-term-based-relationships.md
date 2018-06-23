---
title: 工作 5： 設定以詞彙為主的關聯性 |Microsoft 文件
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6569d512-637d-4f7b-82e1-1e8582278b37
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: b8450d3e77de578810bb57c35aafad6f90c8f19c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36021741"
---
# <a name="task-5-setting-term-based-relationships"></a>工作 5：設定以詞彙為主的關聯
  在這個工作中，您會定義一些以詞彙為主的關聯，值**Supplier Name**網域。 以詞彙為主的關聯可讓您針對屬於定義域值的詞彙進行更正。 它會啟用多個值，這些值除了被視為相同同義字的共同部分拼字以外，都是相同的。 例如， **Inc.** 可以更正為**Incorporated**。 DQS 會在知識探索、清理或比對程序中使用這些關聯。 請參閱[建立以詞彙為主的關聯](http://msdn.microsoft.com/library/hh510404.aspx)如需詳細資訊。  
  
1.  選取**Supplier Name**中**網域清單**。  
  
2.  切換至**以詞彙為主的關聯性**右窗格中的索引標籤。  
  
3.  按一下**加入新關聯性，** 加入至資料表的關聯 工具列上的按鈕。  
  
4.  型別**Co.** 如**值**欄位和**公司**如**更正為**欄位。  
  
5.  針對以下的值重複上述兩個步驟：  
  
    |ReplTest1|更正為|  
    |-----------|----------------|  
    |Corp.|Corporation|  
    |Inc.|Incorporated|  
  
     ![以詞彙關聯](../../2014/tutorials/media/et-settingtermbasedrelations.jpg "詞彙為主的關聯")  
  
## <a name="next-step"></a>下一個步驟  
 [工作 6： 設定同義字](../../2014/tutorials/task-6-setting-synonyms.md)  
  
  
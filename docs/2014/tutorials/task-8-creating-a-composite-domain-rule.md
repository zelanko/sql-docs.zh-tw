---
title: 工作 8： 建立複合定義域規則 |Microsoft 文件
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cff3b662-7876-4445-9bdd-96be35b3ca0c
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 18461e889e56f647b869d2b60cae49d662786160
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145069"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>工作 8：建立複合定義域規則
  在這項工作，您建立的規則**地址驗證**複合定義域。 您會定義跨定義域規則： 如果**縣 （市)** 是**洛杉磯**，**狀態**必須**CA**其中**縣 （市)** 和**狀態**是兩個網域。  
  
1.  在右窗格中，切換至**CD 規則** 索引標籤。  
  
2.  按一下**加入新的定義域規則**從工具列。  
  
3.  型別**City-State Rule**如**名稱**按**ENTER**。  
  
4.  在**建置規則**窗格中，選取**縣 （市)** 網域清單中，選取條件**值等於**和型別**Los Angeles**的值。  
  
5.  在**然後**窗格中，選取**狀態**網域清單中，然後選取**值等於**，型別**CA**值，而且按** 索引標籤**。  
  
     ![複合定義域規則](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "複合定義域規則")  
  
6.  按一下**關閉**頁面，即可切換到 DQS 用戶端主頁面底部的按鈕。 您將會在下一課發行知識庫。 請注意，知識庫處於鎖定狀態 (鎖定圖示)。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 9： 設定參考資料服務](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  
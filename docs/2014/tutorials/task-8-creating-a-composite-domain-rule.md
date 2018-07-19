---
title: 工作 8： 建立複合定義域規則 |Microsoft Docs
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
ms.topic: conceptual
ms.assetid: cff3b662-7876-4445-9bdd-96be35b3ca0c
caps.latest.revision: 7
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7c8779496e3e352a59477cf10f12a13011c5c6b3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189345"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>工作 8：建立複合定義域規則
  在這個工作中，您建立的規則**地址驗證**複合定義域。 您會定義跨定義域規則： 如果**城市**是**Los Angeles**，**狀態**必須是**CA**其中**縣 （市)** 並**狀態**是兩個網域。  
  
1.  在右窗格中，切換至**CD 規則** 索引標籤。  
  
2.  按一下 **加入新的定義域規則**從工具列。  
  
3.  型別**City-State Rule** for**名稱**然後按**ENTER**。  
  
4.  中**建置規則**窗格中，選取**縣 （市)** 網域清單中，選取條件**值等於**並輸入**Los Angeles**的值。  
  
5.  在 **然後**窗格中，選取**狀態**網域 清單中，然後選取**值等於**，類型**CA**的值，然後按** 索引標籤**。  
  
     ![複合定義域規則](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "複合定義域規則")  
  
6.  按一下 **關閉**頁面，即可切換到 DQS 用戶端的主頁面底部的按鈕。 您將會在下一課發行知識庫。 請注意，知識庫處於鎖定狀態 (鎖定圖示)。  
  
## <a name="next-step"></a>下一個步驟  
 [工作 9：設定參考資料服務](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  

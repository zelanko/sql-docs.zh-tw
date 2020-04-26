---
title: 工作8：建立複合定義域規則 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: cff3b662-7876-4445-9bdd-96be35b3ca0c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 7e40ec982a9b2c43c3d55ec60179ac9a0b80e8a1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65489634"
---
# <a name="task-8-creating-a-composite-domain-rule"></a>工作 8：建立複合定義域規則
  在這項工作中，您會建立**位址驗證**複合定義域的規則。 您會定義跨定義域規則：如果**city**是**洛杉磯**，則**state**必須是**CA** ，其中**City**和**State**是兩個網域。  
  
1.  在右窗格中，切換至 [ **CD 規則**] 索引標籤。  
  
2.  按一下工具列中的 [**加入新的定義域規則**]。  
  
3.  輸入「**城市-州**」的**名稱**規則，然後按**enter**鍵。  
  
4.  在 [**建立規則**] 窗格中，選取 [定義域] 清單中的 [ **City** ]，然後選取 [條件**值等於**]，並輸入**洛杉磯**作為值。  
  
5.  在 [ **Then** ] 窗格中，選取 [定義域] 清單中的 [**狀態**]，然後選取 [**值等於**]，輸入**CA**作為值，然後按**tab**鍵。  
  
     ![複合定義域規則](../../2014/tutorials/media/et-creatingacompositedomainrule.jpg "複合定義域規則")  
  
6.  按一下頁面底部的 [**關閉**] 按鈕，切換到 DQS 用戶端的主頁面。 您將會在下一課發行知識庫。 請注意，知識庫處於鎖定狀態 (鎖定圖示)。  
  
## <a name="next-step"></a>後續步驟  
 [工作 9：設定參考資料服務](../../2014/tutorials/task-9-configuring-a-reference-data-service.md)  
  
  

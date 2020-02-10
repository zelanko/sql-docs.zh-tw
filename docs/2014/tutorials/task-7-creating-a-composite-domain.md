---
title: 工作7：建立複合定義域 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bbc00117e10e48adbde37b9f0561610feff8f87e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65488959"
---
# <a name="task-7-creating-a-composite-domain"></a>工作 7：建立複合定義域
  在這項工作中，您會建立複合定義域「**位址驗證**」，其中包含「**位址行**」、「**城市**」、「**州**」和「 **Zip** 」網域。 複合定義域可讓您定義在規則中涉及多個定義域的跨定義域規則。 複合定義域還有其他優點，例如能夠將欄位值剖析成多個定義域。  例如，[完整名稱] 欄位的值可以剖析成個別的名字、中間名和姓氏等定義域。 在本教學課程中，您只會定義跨定義域規則。 如需詳細資訊，請參閱[管理複合定義域](https://msdn.microsoft.com/library/hh510399.aspx)。  
  
1.  在左窗格中，按一下工具列上的 [**建立複合定義域**] 按鈕。  
  
     ![[建立複合定義域] 工具列按鈕](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "[建立複合定義域] 工具列按鈕")  
  
2.  輸入**複合定義功能變數名稱稱**的**位址驗證**。  
  
     ![地址驗證複合定義域](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "地址驗證複合定義域")  
  
3.  從 [網域] 清單中選取 [**位址行**]、[**城市**]、[**州**] 和 [**郵遞區號**]，然後按一下**向右箭**號，將它們加入 [**複合定義域中的定義域**]  
  
4.  按一下 **[確定]** ，關閉對話方塊。  
  
## <a name="next-step"></a>後續步驟  
 [工作 8：建立複合定義域規則](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  

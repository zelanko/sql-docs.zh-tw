---
title: 排序資料行 | Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.sortcolumns.f1
ms.assetid: 66b44b6c-10a5-4e3f-a97b-7568609c88ac
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 0f7cca09018f9486c831e3803aedb5c969c422d1
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769496"
---
# <a name="sort-columns"></a>排序資料行
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[排序資料行]** 對話方塊可讓您根據一或多個資料行排序「複寫監視器」中的方格 (您也可以按一下「複寫監視器」方格中的資料行標頭，針對單一資料行排序)。 例如，若要根據狀態和連接類型排序 **[所有訂閱]** 索引標籤中的訂閱，請遵循下列步驟進行：  
  
1.  在方格的第一個資料列中，從 **[資料行名稱]** 資料行中選取 **[狀態]** ，然後從 **[排序順序]** 資料行中選取值。  
  
2.  在方格的第二個資料列中，從 **[資料行名稱]** 資料行中選取 **[連接類型]** ，然後從 **[排序順序]** 資料行中選取值。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="options"></a>選項。  
 **[狀態]**  
 您想要用來排序的資料行名稱。 您可以針對一或多個資料行進行排序。 不過，您無法針對 **[發行集]** 索引標籤上的 **[目前的平均效能]** 或 **[目前最差效能]** 資料行進行排序，因為這些資料行值的計算方式不同。  
  
 **[排序順序]**  
 請指定 **[遞增]** 或 **[遞減]** 值。  
  
 **全部清除**  
 從排序的方格中移除所有資料列。 若要移除單一資料列，請選取該資料列並按下 Delete 鍵。  
  
## <a name="see-also"></a>另請參閱  
 [監視複寫](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  

---
title: "使用 AddNew 中立即和批次模式 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: ed314bb9-e188-4658-a68c-a2abc49610be
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 32d4298351d214912947ead9322fe1fc5a208eba
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>使用 AddNew 中立即和批次模式
行為**AddNew**方法而定的更新模式**資料錄集**物件和是否傳遞*FieldList*和*值*引數。  
  
 在立即更新模式中 (在其中提供者將變更寫入基礎資料來源一旦呼叫**更新**方法)，則呼叫**AddNew**方法沒有引數集**EditMode**屬性**adEditAdd。** 提供者會快取所有欄位值變更在本機。 呼叫**更新**方法張貼新的記錄，到資料庫，並重設**EditMode**屬性**adEditNone。** 如果您要傳入*FieldList*和*值*引數，ADO 會立即發佈新的記錄，到資料庫 (沒有**更新**呼叫是必要的); **EditMode**屬性值不會變更 (**adEditNone**)。  
  
 在批次更新模式中，呼叫**AddNew**方法沒有引數集**EditMode**屬性**adEditAdd**。 提供者會快取所有欄位值變更在本機。 呼叫**更新**方法會將新的記錄加入至目前**資料錄集**並重設**EditMode**屬性**adEditNone**，但提供者不會將基礎資料庫的變更，直到您呼叫**UpdateBatch**方法。 如果您要傳入*FieldList*和*值*引數，ADO 會將新的記錄傳送至快取中的存放裝置提供者，您必須呼叫**UpdateBatch**張貼新方法記錄至基礎資料庫。 如需有關**更新**和**UpdateBatch**，請參閱[正在更新及保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。


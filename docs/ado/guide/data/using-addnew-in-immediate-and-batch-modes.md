---
title: 使用 AddNew 中即時和批次模式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: ed314bb9-e188-4658-a68c-a2abc49610be
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6295e4499a6f6f25f9111497012f2e9f1d6dc421
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47616647"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>在即時和批次模式中使用 AddNew
行為**AddNew**方法取決於的更新模式**資料錄集**物件和是否傳遞*FieldList*並*值*引數。  
  
 在立即更新模式中 (在其中提供者將變更寫入基礎資料來源之後呼叫**更新**方法)，則呼叫**AddNew**方法，而不需要引數集**EditMode**屬性設**adEditAdd。** 提供者會快取任何欄位值的變更在本機。 呼叫**更新**方法會張貼新的記錄到資料庫，並且重設**EditMode**屬性設**adEditNone。** 如果您傳遞*FieldList*和*值*引數，ADO 會立即發佈新的記錄到資料庫 (沒有**Update**呼叫是必要); **EditMode**屬性值不會變更 (**adEditNone**)。  
  
 在批次更新模式中，呼叫**AddNew**方法沒有引數設定組**EditMode**屬性設**adEditAdd**。 提供者會快取任何欄位值的變更在本機。 呼叫**更新**方法會將新記錄加入至目前**Recordset**並重設**EditMode**屬性設**adEditNone**，但提供者不會張貼至基礎資料庫的變更，直到您呼叫**UpdateBatch**方法。 如果您傳遞*FieldList*並*值*引數，ADO 會將新的記錄傳送至快取中的存放裝置提供者，您必須呼叫**UpdateBatch**張貼新的方法記錄至基礎資料庫。 如需詳細資訊**更新**並**UpdateBatch**，請參閱[正在更新及保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。

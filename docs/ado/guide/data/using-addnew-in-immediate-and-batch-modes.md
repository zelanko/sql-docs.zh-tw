---
title: 在即時和批次模式中使用 AddNew |Microsoft Docs
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
ms.openlocfilehash: 265b1dcd3cdc1aa7f18f0ca54dc2cf54df2da158
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923629"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>在即時和批次模式中使用 AddNew
**AddNew**方法的行為取決於**記錄集**物件的更新模式，以及您是否傳遞*FieldList*和*Values*引數。  
  
 在立即更新模式中（當您呼叫**update**方法時，提供者會將變更寫入基礎資料來源），呼叫不含引數的**AddNew**方法會將**EditMode**屬性設定為**adEditAdd。** 提供者會在本機快取任何域值變更。 呼叫**Update**方法會將新記錄張貼到資料庫，並將**EditMode**屬性重設為**adEditNone。** 如果您傳遞*FieldList*和*Values*引數，ADO 會立即將新記錄張貼到資料庫（不需要**更新**呼叫）;**EditMode**屬性值不會變更（**adEditNone**）。  
  
 在批次更新模式中，呼叫不含引數的**AddNew**方法，會將**EditMode**屬性設定為**adEditAdd**。 提供者會在本機快取任何域值變更。 呼叫**Update**方法會將新記錄加入至目前的**記錄集**，並將**EditMode**屬性重設為**adEditNone**，但提供者不會將變更張貼到基礎資料庫，直到您呼叫**UpdateBatch**方法為止。 如果您傳遞*FieldList*和*Values*引數，ADO 會將新記錄傳送至快取中儲存區的提供者;您必須呼叫**UpdateBatch**方法，將新記錄張貼到基礎資料庫。 如需**Update**和**UpdateBatch**的詳細資訊，請參閱[更新和保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。

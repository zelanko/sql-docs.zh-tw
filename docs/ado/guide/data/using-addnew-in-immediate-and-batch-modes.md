---
title: 在立即和批次模式中使用 AddNew |Microsoft Docs
description: 說明如何在立即和批次模式中使用 AddNew。
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 689b8fbc6c8bb9446adfeb9fec98d53d59b28917
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979049"
---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>在即時和批次模式中使用 AddNew
**AddNew**方法的行為取決於**記錄集**物件的更新模式，以及您是否傳遞*FieldList*和*Values*引數。  
  
 在立即更新模式中 (當您呼叫 **update** 方法) 時，提供者會將變更寫入基礎資料來源中，而呼叫不含引數的 **AddNew** 方法會將 **EditMode** 屬性設定為 **adEditAdd。** 提供者會在本機快取任何域值變更。 呼叫 **Update** 方法會將新記錄張貼至資料庫，並將 **EditMode** 屬性重設為 **adEditNone。** 如果您傳遞 *FieldList* 和 *Values* 引數，ADO 會立即將新記錄張貼至資料庫， (不需要 **更新** 呼叫) ; **EditMode** 屬性值不會變更 (**adEditNone**) 。  
  
 在批次更新模式中，呼叫不含引數的 **AddNew** 方法，會將 **EditMode** 屬性設定為 **adEditAdd**。 提供者會在本機快取任何域值變更。 呼叫 **Update** 方法會將新的記錄加入目前的 **記錄集** ，並將 **EditMode** 屬性重設為 **adEditNone**，但是提供者不會將變更張貼到基礎資料庫，直到您呼叫 **UpdateBatch** 方法為止。 如果您傳遞 *FieldList* 和 *Values* 引數，ADO 會將新記錄傳送給提供者，以便在快取中儲存;您必須呼叫 **UpdateBatch** 方法，以將新記錄張貼到基礎資料庫。 如需 **Update** 和 **UpdateBatch**的詳細資訊，請參閱 [更新和保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。

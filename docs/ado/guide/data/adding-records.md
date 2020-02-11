---
title: 加入記錄 |Microsoft Docs
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
- editing data [ADO], AddNew method
- editing data [ADO], adding data
ms.assetid: dd34669e-6f06-403b-9241-1c85c82aecc2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f4ec0934fbf75de18f460abae84b8117e99f452
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926268"
---
# <a name="adding-records-to-a-recordset"></a>將記錄加入至記錄集
使用**AddNew**方法來建立和初始化現有**記錄集中**的新記錄。 您可以使用**CursorOptionEnum**值為**adAddNew**的**支援**方法，以確認是否可以將記錄加入至目前的**記錄集**物件。

 在您呼叫**AddNew**方法之後，新的記錄就會成為目前的記錄，並在您呼叫**Update**方法之後維持為目前狀態。 如果**記錄集**物件不支援書簽，當您移至另一筆記錄時，您可能無法存取新的記錄。 因此，視您的資料指標類型而定，您可能需要呼叫**Requery**方法，讓新記錄可供存取。

 如果您在編輯目前的記錄或加入新記錄時呼叫**AddNew** ，ADO 會呼叫**Update**方法來儲存任何變更，然後建立新的記錄。

 此章節包含下列主題。

-   [使用 AddNew 新增記錄](../../../ado/guide/data/adding-records-using-addnew.md)

-   [新增多個欄位](../../../ado/guide/data/adding-multiple-fields.md)

-   [判斷編輯模式](../../../ado/guide/data/determining-edit-mode.md)

-   [在即時和批次模式中使用 AddNew](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)

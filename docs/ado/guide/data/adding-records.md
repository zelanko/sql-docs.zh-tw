---
title: "加入資料錄 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- editing data [ADO], AddNew method
- editing data [ADO], adding data
ms.assetid: dd34669e-6f06-403b-9241-1c85c82aecc2
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1d46cb8e801f39cf8b87c0c3187667247e3da9d0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="adding-records-to-a-recordset"></a>將記錄加入至資料錄集
使用**AddNew**方法來建立並初始化新的記錄中的現有**資料錄集**。 您可以使用**支援**方法**CursorOptionEnum**值**adAddNew**以確認是否可以將記錄加入至目前**資料錄集**物件。

 在您呼叫後**AddNew**方法，新的記錄變成目前的記錄，並且目前之後呼叫**更新**方法。 如果**資料錄集**物件不支援書籤，您可能無法存取新的記錄，一旦您移到另一筆記錄。 因此，根據您的資料指標類型，您可能需要呼叫**Requery** ，使新的記錄可存取的方法。

 如果您呼叫**AddNew** ADO 編輯目前的記錄時，或加入新的記錄時，呼叫**更新**方法來儲存任何變更，並接著會建立新的記錄。

 此章節包含下列主題。

-   [使用 AddNew 新增記錄](../../../ado/guide/data/adding-records-using-addnew.md)

-   [新增多個欄位](../../../ado/guide/data/adding-multiple-fields.md)

-   [判斷編輯模式](../../../ado/guide/data/determining-edit-mode.md)

-   [在即時和批次模式中使用 AddNew](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)

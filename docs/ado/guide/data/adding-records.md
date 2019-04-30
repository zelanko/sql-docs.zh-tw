---
title: 新增記錄 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: a17e09df7c7235e1361aae79bd89152c290b1bdb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294398"
---
# <a name="adding-records-to-a-recordset"></a>將記錄新增至資料錄集
使用**AddNew**方法來建立並初始化新的記錄中的現有**資料錄集**。 您可以使用**支援**方法**CursorOptionEnum**的值**adAddNew**若要確認是否可以將記錄加入至目前**資料錄集**物件。

 在您呼叫後**AddNew**方法，新的記錄就會成為目前的記錄，並保持最新呼叫之後**更新**方法。 如果**資料錄集**物件不支援書籤，您可能無法存取新的記錄，一旦您移到另一筆記錄。 因此，根據您的資料指標類型，您可能需要呼叫**Requery**方法，以供新的記錄。

 如果您呼叫**AddNew** ADO 編輯目前的記錄時，或加入新的記錄時，呼叫**更新**方法來儲存任何變更，並接著會建立新的記錄。

 此章節包含下列主題。

-   [使用 AddNew 新增記錄](../../../ado/guide/data/adding-records-using-addnew.md)

-   [新增多個欄位](../../../ado/guide/data/adding-multiple-fields.md)

-   [判斷編輯模式](../../../ado/guide/data/determining-edit-mode.md)

-   [在即時和批次模式中使用 AddNew](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)

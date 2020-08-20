---
description: 將記錄加入至記錄集
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2394cf5612dab45ccd2e0f3cc6e2204b6d451142
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453880"
---
# <a name="adding-records-to-a-recordset"></a>將記錄加入至記錄集
使用 **AddNew** 方法，在現有的 **記錄集中**建立和初始化新的記錄。 您可以使用**CursorOptionEnum**值為**adAddNew**的**支援**方法，確認是否可以將記錄加入至目前的**記錄集**物件。

 在您呼叫 **AddNew** 方法之後，新的記錄會成為目前的記錄，並在您呼叫 **Update** 方法之後保持最新狀態。 如果 **記錄集** 物件不支援書簽，當您移到另一筆記錄時，可能無法存取新的記錄。 因此，視資料指標類型而定，您可能需要呼叫 **Requery** 方法來讓新記錄變成可存取。

 如果您在編輯目前的記錄或加入新記錄時呼叫 **AddNew** ，ADO 會呼叫 **Update** 方法來儲存任何變更，然後建立新的記錄。

 此章節包含下列主題。

-   [使用 AddNew 新增記錄](../../../ado/guide/data/adding-records-using-addnew.md)

-   [新增多個欄位](../../../ado/guide/data/adding-multiple-fields.md)

-   [判斷編輯模式](../../../ado/guide/data/determining-edit-mode.md)

-   [在即時和批次模式中使用 AddNew](../../../ado/guide/data/using-addnew-in-immediate-and-batch-modes.md)

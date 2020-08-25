---
description: 預期的錯誤
title: 預期的錯誤 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
author: rothja
ms.author: jroth
ms.openlocfilehash: a85d313dabe9c6c0cf8c4dcdb76e01b0f2962d7d
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806403"
---
# <a name="anticipating-errors"></a>預期的錯誤
錯誤防護至少與錯誤處理一樣重要。 最後一節包含您的應用程式可採取的一些預防措施，以協助讓錯誤更不可能發生。  
  
 檢查物件的狀態，方法是在嘗試使用這些物件執行作業之前，先檢查 **state** 屬性中的值。 例如，如果您的應用程式使用全域 **連接**，請檢查其 **狀態** 屬性，以查看它是否已在呼叫 **open** 方法之前開啟。  
  
-   接受使用者資料的任何程式都必須包含程式碼，才能在將資料傳送至資料存放區之前先驗證該資料。 您無法依賴資料存放區、提供者、ADO 或甚至是您的程式設計語言，來通知您有問題。 您必須檢查使用者輸入的每個位元組，確定資料是其欄位的正確類型，而且所需的欄位不是空的。  
  
 請先檢查資料，然後再嘗試將任何資料寫入資料存放區。 最簡單的方式是處理 **WillMove** 事件或 **WillUpdateRecordset** 事件。 如需處理 ADO 事件的更完整討論，請參閱 [處理 Ado 事件](./handling-ado-events.md)。  
  
 嘗試移動記錄指標之前，請確定 **記錄集** 物件不在 **記錄集** 界限之外。 如果您嘗試 **MoveNext** **EOF** 為 true 或 **MovePrev** ，當 **BOF** 為 true 時，將會發生錯誤。 如果您在**EOF**和**BOF**都為 True 時執行任何**移動**方法，則會產生錯誤。  
  
 如果您嘗試在空的**記錄集**上執行**搜尋**和**尋找**等作業，也會發生錯誤。
---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6e555f00964ae6bdc7eb91a8701f2447d91b37d3
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702406"
---
# <a name="anticipating-errors"></a>預期的錯誤
錯誤預防是至少和錯誤處理一樣重要。 最後一節中包含一份您的應用程式可以為了讓比較不可能出現的錯誤所採取的預防措施。  
  
 簽入的值來檢查物件的狀態**狀態**然後再嘗試執行作業使用這些物件的屬性。 例如，如果您的應用程式會使用全域**連接**，檢查其**狀態**屬性，以查看它是否已開啟，再呼叫**開啟**方法。  
  
-   接受來自使用者資料的任何程式都必須包含程式碼，以驗證該資料，再將它傳送到資料存放區。 您不能依賴資料存放區、 提供者、 ADO 中或甚至是您的程式語言，通知您的問題。 您必須檢查輸入您的使用者，並確定資料是正確的型別，它的欄位和必要的欄位不是空白的每個位元組。  
  
 您嘗試寫入資料存放區中的任何資料之前，請檢查的資料。 若要這樣做最簡單方式是以處理**WillMove**事件或**WillUpdateRecordset**事件。 處理 ADO 事件的更完整討論，請參閱[處理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)。  
  
 請確定**資料錄集**以外的範圍不是物件**資料錄集**之前嘗試移動的記錄指標。 如果您嘗試**MoveNext**當**EOF**為 True 或**MovePrev**當**BOF**為 True 時，會發生錯誤。 如果您執行的任何**移動**方法時同時**EOF**並**BOF**為 True，會產生錯誤。  
  
 也會發生錯誤如果您嘗試執行作業，例如**Seek**並**尋找**上空白**資料錄集**。

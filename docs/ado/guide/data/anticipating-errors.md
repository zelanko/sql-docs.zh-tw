---
title: "預計錯誤 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- anticipating errors [ADO]
- errors [ADO], preventing
- preventing errors [ADO]
ms.assetid: ea1d4a97-58c3-476b-a496-cc80db2a90d5
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4b7642e4dabebe3db00cb4852d2efea43269cef8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="anticipating-errors"></a>預期的錯誤
錯誤預防為至少和錯誤處理一樣重要。 這最後一節包含您的應用程式可以為了讓比較不可能發生的錯誤採取預防措施的簡短清單。  
  
 檢查物件的狀態檢查的值**狀態**然後再嘗試執行作業使用這些物件的屬性。 例如，如果您的應用程式會使用全域**連接**，檢查其**狀態**屬性來查看它是否已開啟，然後再呼叫**開啟**方法。  
  
-   接受來自使用者資料的任何程式必須包含的程式碼再將它傳送到資料存放區驗證該資料。 您不能依賴資料存放區、 提供者、 ADO 中或甚至您的程式語言，通知您的問題。 您必須檢查每個位元組，輸入您的使用者，並確定資料是正確的型別，它的欄位，而且必要的欄位不是空的。  
  
 您嘗試寫入資料存放區中的任何資料之前，請檢查資料。 若要這樣做最簡單的方式是處理**WillMove**事件或**WillUpdateRecordset**事件。 處理 ADO 事件的更完整討論，請參閱[處理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)。  
  
 請確定**資料錄集**物件不超過界限**資料錄集**嘗試移動的記錄指標。 如果您嘗試**MoveNext**時**EOF**為 True 或**MovePrev**時**BOF**為 True 時，會發生錯誤。 如果您執行的任何**移動**方法時同時**EOF**和**BOF**為 True，會產生錯誤。  
  
 也會發生錯誤如果您嘗試執行作業，例如**搜尋**和**尋找**上空**資料錄集**。

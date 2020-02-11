---
title: 預見錯誤 |Microsoft Docs
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
ms.openlocfilehash: 2d92d96e3b8cdfea5cacea35d852e8859de65dbd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925988"
---
# <a name="anticipating-errors"></a>預期的錯誤
錯誤防護的重要性至少與錯誤處理相同。 最後一節包含您的應用程式可以採取的預防措施簡短清單，以協助避免發生錯誤。  
  
 嘗試使用這些物件執行作業之前，請先檢查**state**屬性中的值，檢查物件的狀態。 例如，如果您的應用程式使用全域**連接**，請檢查其**State**屬性，以查看它是否已經開啟，然後再呼叫**open**方法。  
  
-   接受使用者資料的任何程式都必須包含驗證該資料的程式碼，然後再將它傳送至資料存放區。 您不能依賴資料存放區、提供者、ADO，甚至是您的程式設計語言來通知您問題。 您必須檢查使用者輸入的每個位元組，以確保資料的欄位是正確的類型，而且必要的欄位不是空的。  
  
 嘗試將任何資料寫入資料存放區之前，請先檢查資料。 若要這麼做，最簡單的方式是處理**WillMove**事件或**WillUpdateRecordset**事件。 如需處理 ADO 事件的更完整討論，請參閱[處理 Ado 事件](../../../ado/guide/data/handling-ado-events.md)。  
  
 嘗試移動記錄指標之前，請確定**記錄集**物件不在**記錄集**的界限之外。 如果您嘗試**在當** **BOF**為 true 時執行**MoveNext**或**MovePrev** ，則會發生錯誤。 如果當**EOF**和**BOF**都是 True 時，執行任何**Move**方法，就會產生錯誤。  
  
 如果您嘗試在空的**記錄集**上執行**搜尋**和**尋找**之類的作業，也會發生錯誤。

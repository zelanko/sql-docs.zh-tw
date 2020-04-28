---
title: 錯誤處理 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4cb3213b6a4c5711ccb8d6f9243047d8361a6e37
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925429"
---
# <a name="error-handling"></a>錯誤處理
ADO 會使用數種不同的方法來通知應用程式發生錯誤。 本節將討論當您使用 ADO 時可能發生的錯誤類型，以及應用程式的通知方式。 最後，我們會提出有關如何處理這些錯誤的建議。  
  
## <a name="how-does-ado-report-errors"></a>ADO 如何報告錯誤？  
 ADO 會以數種方式通知您錯誤：  
  
-   ADO 錯誤會產生執行階段錯誤。 以與任何其他執行時間錯誤相同的方式處理 ADO 錯誤，例如在 Visual Basic 中使用**On error**語句。  
  
-   您的程式可能會收到來自 OLE DB 的錯誤。 OLE DB 錯誤也會產生執行階段錯誤。  
  
-   如果錯誤是您的資料提供者所特有，則在發生錯誤時，會在用來存取資料存放區的**連接**物件的**Errors**集合中放置一或多個**錯誤**物件。  
  
-   如果引發事件的進程也產生錯誤，錯誤資訊會放在**錯誤**物件中，並以參數的形式傳遞至事件。 如需事件的詳細資訊，請參閱[處理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)。  
  
-   處理批次更新或涉及**記錄集**的其他大量作業時所發生的問題，可以由**記錄集**的**Status**屬性來表示。 例如， **RecordStatusEnum**值可以指定架構條件約束違規或許可權不足。  
  
-   與目前記錄中的特定**欄位**相關的問題，也會以**記錄**或**記錄集**之**Fields**集合中每個**欄位**的**Status**屬性來表示。 例如，無法完成或不相容資料類型的更新可以由**FieldStatusEnum**值指定。  
  
 此章節包含下列主題。  
  
-   [ADO 錯誤](../../../ado/guide/data/ado-errors.md)  
  
-   [提供者錯誤](../../../ado/guide/data/provider-errors.md)  
  
-   [欄位相關的錯誤資訊](../../../ado/guide/data/field-related-error-information.md)  
  
-   [資料錄集相關的錯誤資訊](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [處理其他語言的錯誤](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [預期的錯誤](../../../ado/guide/data/anticipating-errors.md)

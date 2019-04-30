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
manager: craigg
ms.openlocfilehash: 5d8f96b28a15258df4b7d093ce14f227f28ad9b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161743"
---
# <a name="error-handling"></a>錯誤處理
ADO 使用多種不同的方法來通知發生之錯誤的應用程式。 本節討論當您使用 ADO 和您的應用程式接收通知的方式可能會發生的錯誤類型。 它做出結論，提出有關如何處理這些錯誤的建議。  
  
## <a name="how-does-ado-report-errors"></a>ADO 如何回報錯誤？  
 ADO 錯誤進行通知您透過數種方式：  
  
-   ADO 錯誤會產生執行階段錯誤。 就像任何其他執行階段錯誤，例如使用的相同方式處理 ADO 錯誤**On Error** Visual Basic 中的陳述式。  
  
-   您的程式可以接收來自 OLE DB 的錯誤。 OLE DB 錯誤產生的執行階段錯誤。  
  
-   如果錯誤是一或多個您的資料提供者特有**錯誤**物件置於**錯誤**集合**連接**用來存取資料的物件發生錯誤時的存放區。  
  
-   如果引發事件的處理程序也會產生錯誤，錯誤資訊會置於**錯誤**物件，並做為參數傳遞至事件。 請參閱[處理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)如需事件的詳細資訊。  
  
-   更新或其他涉及的大量作業的批次時處理發生的問題**Recordset**可以由**狀態**屬性**資料錄集**。 例如，藉由指定結構描述條件約束違規或權限不足**RecordStatusEnum**值。  
  
-   發生涉及為特定的問題**欄位**目前的記錄中也由**狀態**屬性的每個**欄位**中**欄位**的集合**記錄**或是**資料錄集**。 例如，藉由指定無法完成的更新] 或 [不相容的資料類型**FieldStatusEnum**值。  
  
 此章節包含下列主題。  
  
-   [ADO 錯誤](../../../ado/guide/data/ado-errors.md)  
  
-   [提供者錯誤](../../../ado/guide/data/provider-errors.md)  
  
-   [欄位相關的錯誤資訊](../../../ado/guide/data/field-related-error-information.md)  
  
-   [資料錄集相關的錯誤資訊](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [處理其他語言的錯誤](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [預期的錯誤](../../../ado/guide/data/anticipating-errors.md)

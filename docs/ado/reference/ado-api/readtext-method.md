---
title: ReadText 方法 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7c3e2dcf695e9c6748881656d87e02404209dbf
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280777"
---
# <a name="readtext-method"></a>ReadText 方法
讀取指定文字的字元數[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>參數  
 *NumChars*  
 選擇性。 A**長**值，指定要從檔案讀取的字元數或[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)值。 預設值是**adReadAll**。  
  
## <a name="return-value"></a>傳回值  
 **ReadText**方法會讀取指定的字元數、 整行或整個資料流，從**資料流**物件，並傳回產生的字串。  
  
## <a name="remarks"></a>備註  
 如果*NumChar*的字元數超過保留的資料流中，會傳回只將剩餘的字元。 讀取的字串不會填補到符合所指定的長度*NumChar*。 如果沒有左讀取的字元，則會傳回的 variant，其值為 null。 **ReadText**無法用來讀取回溯。  
  
> [!NOTE]
>  **ReadText**方法配合文字資料流 ([類型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 二進位資料流 (**類型**是**adTypeBinary**)，使用[讀取](../../../ado/reference/ado-api/read-method.md)。  
  
 查詢，導致大量的 XML 資料，傳回透過**ReadText** ActiveX Data Object (ADO) 資料流物件的方法可能需要大量時間來執行; 如果這是從叫用 COM + 元件ASP 網頁在使用者工作階段可能會逾時。ADO 將從 Unicode，utf-8 編碼方式轉換資料流物件資料參與的這類數量龐大的資料轉換次記憶體頻繁的重新配置是很耗時。 若要解決，請重複的呼叫**ReadText**方法之 ADO 命令物件，並指定較少的字元。 測試顯示值等於 128k (131,072) 是最佳的。 回應時間減少這個值會減少。 如需詳細資訊，請參閱知識庫文章 280067，"PRB： 使用 ADO 資料流物件 ReadText 方法來擷取從 SQL Server 2000 的非常大型的 XML 文件可能會很慢 」，Microsoft 知識庫中在 http://support.microsoft.com 。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Read 方法](../../../ado/reference/ado-api/read-method.md)

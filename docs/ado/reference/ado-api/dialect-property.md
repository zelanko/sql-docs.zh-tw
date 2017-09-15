---
title: "方言屬性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Command::Dialect
helpviewer_keywords:
- Dialect property
ms.assetid: 329c3a71-ba88-4009-b04f-2f52195a5957
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 73c7dfd6fe5aec706d5e27ce6d55f489285748c4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="dialect-property"></a>方言屬性
指出的方言[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性。 方言定義的語法和一般的規則，提供者用來剖析字串或資料流。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 **方言**屬性包含有效的 GUID，代表命令文字或資料流的方言。 這個屬性的預設值為 {C8B521FB-5CF3-11CE-ADE5-00AA0044773D}，這表示，提供者應該選擇如何解譯命令文字或資料流。  
  
## <a name="remarks"></a>備註  
 ADO 不會查詢提供者，當使用者讀取此屬性; 的值它會傳回目前儲存的值的字串表示[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。  
  
 當使用者設定**方言**屬性，ADO 會驗證 GUID，並引發錯誤，如果所提供的值不是有效的 GUID。 請參閱您的提供者，以判斷支援的 GUID 值的文件**方言**屬性。  
  
## <a name="applies-to"></a>適用於  
 [命令物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Execute 方法 （ADO 命令中）](../../../ado/reference/ado-api/execute-method-ado-command.md)

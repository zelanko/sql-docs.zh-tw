---
title: Dialect 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::Dialect
helpviewer_keywords:
- Dialect property
ms.assetid: 329c3a71-ba88-4009-b04f-2f52195a5957
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5c7e6aab3e3b33d02adcb067fff46b49973191b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698241"
---
# <a name="dialect-property"></a>Dialect 屬性
指出的方言[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)或是[CommandStream](../../../ado/reference/ado-api/commandstream-property-ado.md)屬性。 方言定義的語法和一般提供者剖析字串或資料流時所使用的規則。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 **方言**屬性包含有效的 GUID，代表命令文字或資料流的方言。 這個屬性的預設值是 {C8B521FB-5CF3-11CE-ADE5-00AA0044773D}，表示提供者應該選擇如何解譯命令文字或資料流。  
  
## <a name="remarks"></a>備註  
 ADO 不會查詢提供者，當使用者讀取此屬性; 的值它會傳回目前儲存的值的字串表示[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。  
  
 當使用者設定**方言**屬性，ADO 會驗證 GUID，並會引發錯誤，如果所提供的值不是有效的 GUID。 請參閱您的提供者，以判斷所支援的 GUID 值的文件**方言**屬性。  
  
## <a name="applies-to"></a>適用於  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Execute 方法 (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)

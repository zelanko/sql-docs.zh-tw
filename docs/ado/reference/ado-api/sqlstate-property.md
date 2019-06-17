---
title: SQLState 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9e4804b5cbdec4008e1c967b81620ea96eead924
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711321"
---
# <a name="sqlstate-property"></a>SQLState 屬性
表示 SQL 狀態給定[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回五字元**字串**遵循 ANSI SQL 標準，並指出錯誤的程式碼的值。  
  
## <a name="remarks"></a>備註  
 使用**SQLState**讀取提供者會傳回 SQL 陳述式處理期間發生錯誤時的五個字元的錯誤程式碼的屬性。 比方說，當使用 Microsoft OLE DB Provider for ODBC，與 Microsoft SQL Server 資料庫，SQL 狀態錯誤碼源自 ODBC，根據特定 ODBC 錯誤或錯誤，源自於 Microsoft SQL Server，並接著會對應到 ODBC錯誤。 這些錯誤碼都記載於 ANSI SQL 標準，但可能由不同的資料來源以不同的方式實作。  
  
## <a name="applies-to"></a>適用於  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   

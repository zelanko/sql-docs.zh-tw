---
title: "SQLState 屬性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f65624cc9393a1ce676530102d41eb1655bcf79b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlstate-property"></a>SQLState 屬性
表示 SQL 狀態給定[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回五字元**字串**遵循 ANSI SQL 標準，並指出錯誤的程式碼的值。  
  
## <a name="remarks"></a>備註  
 使用**SQLState**讀取提供者會傳回 SQL 陳述式的處理期間發生錯誤時的五個字元的錯誤程式碼的屬性。 例如，當 Microsoft OLE DB Provider for ODBC 使用 Microsoft SQL Server 資料庫，SQL 狀態錯誤碼源自 ODBC，根據 ODBC 相關的錯誤或錯誤，是來自 Microsoft SQL Server，並接著會對應到 ODBC發生錯誤。 這些錯誤碼會記載於 ANSI SQL 標準，但可能由不同的資料來源以不同的方式實作。  
  
## <a name="applies-to"></a>適用於  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [描述、 HelpContext、 說明檔案、 NativeError、 數字、 來源和 SQLState 屬性範例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 說明檔案、 NativeError、 數字、 來源和 SQLState 屬性範例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   


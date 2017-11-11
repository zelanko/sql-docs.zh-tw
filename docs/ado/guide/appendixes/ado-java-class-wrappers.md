---
title: "ADO Java 類別包裝函式 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 08cbd288ba9f64816ae0c8fd62c18171967c4d0d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="ado-java-class-wrappers"></a>ADO Java 類別包裝函式
此程式碼會宣告物件的執行個體[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)類別包裝函式與它初始化，在相同的程式碼行。 此外，它會宣告變數中的引數的每個[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法，特別是針對[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)和[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) （因為不支援 Java 列舉型別）。 它會開啟並關閉**資料錄集**物件。 只設定為 NULL 的 Rs1 排程 Java 執行其系統化且短暫的版本的未使用的物件時釋放該變數。  
  
```  
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 Microsoft SDK for Java](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)


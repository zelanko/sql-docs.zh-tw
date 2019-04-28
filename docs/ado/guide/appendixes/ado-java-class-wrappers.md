---
title: ADO Java 類別包裝函式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ddcbba246f0bdcfb5c3a22766f5d335a2bd5893e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62719970"
---
# <a name="ado-java-class-wrappers"></a>ADO Java 類別包裝函式
此程式碼會宣告執行個體的 ADO[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)類別包裝函式和初始化，全部在同一行程式碼。 此外，它會宣告變數中的引數的每個[開放](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法，特別是針對[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)並[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) （因為 Java 不支援列舉型別）。 它會開啟並關閉**資料錄集**物件。 只設定為 NULL 的 Rs1 排程 Java 執行其系統化和間歇性版未使用的物件時釋放該變數。  
  
```java
public static void main( String args[])  
{  
   msado15._Recordset   Rs1 = new msado15.Recordset();  
   Variant Source     = new Variant( "SELECT * FROM Authors" );  
   Variant Connect    = new Variant( "DSN=AdoDemo;UID=admin;PWD=;" );  
   int     LockType   = msado15.CursorTypeEnum.adOpenForwardOnly;  
   int     CursorType = msado15.LockTypeEnum.adLockReadOnly;  
   int     Options    = -1;  
  
   Rs1.Open( Source, Connect, LockType,  CursorType, Options );  
   Rs1.Close();  
   Rs1 = null;  
  
   System.out.println( "Success!\n" );  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 Microsoft SDK for Java](../../../ado/guide/appendixes/using-the-microsoft-sdk-for-java.md)

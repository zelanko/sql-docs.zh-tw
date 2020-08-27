---
description: ADO Java 類別包裝函式
title: ADO JAVA 類別包裝函式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- class wrappers [ADO]
ms.assetid: 1fc09dc1-9e32-412e-9f43-b8eb8bb483ca
author: rothja
ms.author: jroth
ms.openlocfilehash: 1694c3782aa57993cee39ea4f449e7b280fccdf6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991188"
---
# <a name="ado-java-class-wrappers"></a>ADO Java 類別包裝函式
這段程式碼會宣告 ADO [記錄集](../../reference/ado-api/recordset-object-ado.md) 類別包裝函式的實例，並將它初始化，全都在同一行程式碼上。 此外，它會針對 [Open](../../reference/ado-api/open-method-ado-recordset.md) 方法中的每個引數宣告變數，特別是針對 [LockType](../../reference/ado-api/locktype-property-ado.md) 和 [CursorType](../../reference/ado-api/cursortype-property-ado.md) (，因為 JAVA 不支援) 的列舉類型。 它會開啟並關閉 **記錄集** 物件。 將 Rs1 設定為 Null 只會排程要在 JAVA 執行其系統化和間歇性釋放未使用物件時釋放的變數。  
  
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
 [使用 Microsoft SDK for Java](./using-the-microsoft-sdk-for-java.md)
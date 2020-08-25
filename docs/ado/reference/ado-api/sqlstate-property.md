---
description: SQLState 屬性
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 65d72fed54723f525f4e1426ed04886e9d474985
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777367"
---
# <a name="sqlstate-property"></a>SQLState 屬性
表示指定 [錯誤](./error-object.md) 物件的 SQL 狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回五個字元的 **字串** 值，此值會遵循 ANSI SQL 標準，並指出錯誤碼。  
  
## <a name="remarks"></a>備註  
 使用 **SQLState** 屬性，即可讀取在處理 SQL 語句期間發生錯誤時，提供者所傳回的五個字元錯誤碼。 例如，搭配使用 Microsoft OLE DB Provider for ODBC 與 Microsoft SQL Server 資料庫時，SQL 狀態錯誤碼是源自 ODBC，根據 ODBC 特定的錯誤或源自 Microsoft SQL Server 的錯誤，然後對應至 ODBC 錯誤。 這些錯誤碼記載在 ANSI SQL 標準中，但可能會因不同的資料來源而以不同方式執行。  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](./error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、NativeError、Number、Source 和 SQLState 屬性範例 (VB) ](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [ (VC + +) 的 Description、HelpCoNtext、説明、NativeError、Number、Source 和 SQLState 屬性範例 ](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)
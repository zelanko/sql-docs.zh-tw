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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9b40c35730b02352f1e8667941aa4c220a7ad4df
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759764"
---
# <a name="sqlstate-property"></a>SQLState 屬性
指出給定[錯誤](../../../ado/reference/ado-api/error-object.md)物件的 SQL 狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回遵循 ANSI SQL 標準的五個字元**字串**值，並指出錯誤碼。  
  
## <a name="remarks"></a>備註  
 使用**SQLState**屬性可讀取在處理 SQL 語句期間發生錯誤時，提供者所傳回的五個字元錯誤碼。 例如，搭配 Microsoft SQL Server 資料庫使用適用于 ODBC 的 Microsoft OLE DB 提供者時，SQL 狀態錯誤碼會根據 ODBC 特定的錯誤或源自 Microsoft SQL Server 的錯誤而產生，然後對應至 ODBC 錯誤。 這些錯誤碼記載在 ANSI SQL 標準中，但可能會因不同的資料來源而以不同的方式執行。  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、內容説明、NativeError、Number、Source 和 SQLState 屬性範例（VB）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpCoNtext、內容説明、NativeError、Number、Source 和 SQLState 屬性範例（VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   

---
title: 檔案為基礎的驅動程式診斷範例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: decb09098cee4b9ab6473e3c622b9917a89e9b09
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809316"
---
# <a name="file-based-driver-diagnostic-example"></a>以檔案為基礎的驅動程式診斷範例
檔案為基礎的驅動程式會做為 ODBC 驅動程式和資料來源。 在 ODBC 連接，並做為資料來源，它會因此產生錯誤和警告，同時做為元件。 此外，它會是介面驅動程式管理員使用的元件，因為它格式化，並傳回引數**SQLGetDiagRec**。  
  
 比方說，如果 Microsoft® dBASE 驅動程式無法配置足夠的記憶體，它可能會傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 此錯誤並不相關的資料來源，因為驅動程式只加入前置詞診斷訊息 ([Microsoft]) 的廠商和驅動程式 ([ODBC dBASE 驅動程式])。  
  
 如果驅動程式找不到檔案 Employee.dbf，它可能會傳回下列值從**SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 此錯誤與資料來源，因為驅動程式加入資料來源 ([dBASE]) 的檔案格式做為前置詞的診斷訊息。 由於驅動程式也是與資料來源所使用的元件，它會新增前置詞 ([Microsoft]) 的廠商和驅動程式 ([ODBC dBASE 驅動程式])。

---
description: 以檔案為基礎的驅動程式診斷範例
title: 以檔案為基礎的驅動程式診斷範例 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8986ebaa8c4ecf0ac18f4e043eb731df35054884
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499858"
---
# <a name="file-based-driver-diagnostic-example"></a>以檔案為基礎的驅動程式診斷範例
以檔案為基礎的驅動程式，可作為 ODBC 驅動程式和資料來源。 因此，它可能會產生錯誤和警告，作為 ODBC 連接和資料來源中的元件。 因為它也是與驅動程式管理員互動的元件，所以它會格式化並傳回 **SQLGetDiagRec**的引數。  
  
 例如，如果 Microsoft® driver for dBASE 無法配置足夠的記憶體，它可能會從 **SQLGetDiagRec**傳回下列值：  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 因為此錯誤與資料來源無關，所以驅動程式只會將前置詞新增至廠商 ( [Microsoft] ) 的診斷訊息，以及 ( [ODBC dBASE 驅動程式] ) 的驅動程式。  
  
 如果驅動程式找不到該檔案，則可能會從 **SQLGetDiagRec**傳回下列值：  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 因為此錯誤與資料來源有關，所以驅動程式會將資料來源 ( [dBASE] ) 的檔案格式加入至診斷訊息的前置詞。 因為驅動程式也是與資料來源介面的元件，所以它會為廠商新增前置詞 ( [Microsoft] ) 和驅動程式 ( [ODBC dBASE 驅動程式] ) 。

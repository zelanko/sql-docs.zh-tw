---
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
ms.openlocfilehash: 6f09e4f4758b6276836b08f02b24fb31dd1fadc7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305636"
---
# <a name="file-based-driver-diagnostic-example"></a>以檔案為基礎的驅動程式診斷範例
以檔案為基礎的驅動程式會同時做為 ODBC 驅動程式和資料來源。 因此，它可能會產生錯誤和警告，做為 ODBC 連接和資料來源中的元件。 因為它也是與驅動程式管理員介面的元件，所以它會格式化並傳回**SQLGetDiagRec**的引數。  
  
 例如，如果適用于 dBASE 的 Microsoft®驅動程式無法配置足夠的記憶體，它可能會從**SQLGetDiagRec**傳回下列值：  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 因為此錯誤與資料來源無關，所以驅動程式只會將前置詞新增至廠商的診斷訊息（[Microsoft]）和驅動程式（[ODBC dBASE 驅動程式]）。  
  
 如果驅動程式找不到檔案 Employee，它可能會從**SQLGetDiagRec**傳回下列值：  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 由於此錯誤與資料來源相關，因此驅動程式已將資料來源的檔案格式（[dBASE]）新增為診斷訊息的前置詞。 因為驅動程式也是與資料來源介面的元件，所以它會為廠商（[Microsoft]）和驅動程式（[ODBC dBASE 驅動程式]）新增前置詞。

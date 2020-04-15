---
title: 使用儲存過程時撤銷和授予許可權 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 469e6f0fdc6794e3bd163844e43821798aa4a617
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303984"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>在使用預存程序時撤銷和授與權限
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 當授予使用者權限然後在儲存過程存取的表上復原時,Oracle 的 Microsoft ODBC 驅動程式將傳回以下錯誤訊息:  
  
 SQL_ERROR=-1  
  
 szErrorMsg_"[微軟][Oracle的ODBC驅動程式]錯誤數量的參數"  
  
 szErrorMsg_"[微軟][Oracle的ODBC驅動程式]語法錯誤或訪問衝突"  
  
 在這種情況下,對 Oracle OCI 函數 Odessp() 的調用失敗,但為了實現預設參數是必要的。 修改基礎表許可權后,必須先重新編譯存儲過程,然後再運行它。

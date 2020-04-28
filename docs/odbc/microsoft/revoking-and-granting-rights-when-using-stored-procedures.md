---
title: 使用預存程式時撤銷和授與許可權 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303984"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>在使用預存程序時撤銷和授與權限
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 當授與使用者權限，然後撤銷預存程式所存取的資料表時，Microsoft ODBC Driver for Oracle 會傳回下列錯誤訊息：  
  
 SQL_ERROR =-1  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 錯誤的參數數目"  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 語法錯誤或存取違規"  
  
 在此情況下，對 Oracle OCI 函數 Odessp （）的呼叫會失敗，但必須要有才能執行預設參數。 修改基礎資料表許可權之後，必須重新編譯預存程式，然後再執行一次。

---
title: 撤銷和授與權限，當使用預存程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91fcf722554fe1840465329e707c792a6bbab6db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987950"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>在使用預存程序時撤銷和授與權限
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 Microsoft ODBC Driver for Oracle 授與且然後撤銷預存程序所存取的資料表上的使用者權限時，會傳回下列錯誤訊息：  
  
 SQL_ERROR=-1  
  
 szErrorMsg ="[Microsoft] [ODBC driver for Oracle] 參數數目不正確 」  
  
 szErrorMsg ="[Microsoft] [ODBC driver for Oracle] 語法錯誤或存取違規 」  
  
 呼叫 Oracle OCI 函式 Odessp() 在此情況下失敗，但會需要實作預設參數。 修改基礎資料表的權限之後，就必須重新編譯預存程序才能再次執行它。

---
title: "撤銷及授與權限，當使用預存程序 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5c82fc5db88bae5cb02d3fd7bf5164b775484a25
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>撤銷與授與權限時使用預存程序
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 當使用者權限授與，而被撤銷預存程序所存取的資料表上，Microsoft ODBC Driver for Oracle 傳回下列錯誤訊息：  
  
 SQL_ERROR = 1  
  
 szErrorMsg ="[Microsoft] [oracle 的 ODBC 驅動程式] 的參數數目錯誤 」  
  
 szErrorMsg = 「 [Microsoft] [oracle 的 ODBC 驅動程式] 語法錯誤或存取違規 」  
  
 呼叫 Oracle OCI 函式 Odessp() 無法在此案例中，但會需要實作預設參數。 修改基礎資料表的權限之後，就必須重新編譯預存程序之前執行一次。

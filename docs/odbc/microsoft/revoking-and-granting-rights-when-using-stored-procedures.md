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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91fcf722554fe1840465329e707c792a6bbab6db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987950"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>在使用預存程序時撤銷和授與權限
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 當授與使用者權限，然後撤銷預存程式所存取的資料表時，Microsoft ODBC Driver for Oracle 會傳回下列錯誤訊息：  
  
 SQL_ERROR =-1  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 錯誤的參數數目"  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 語法錯誤或存取違規"  
  
 在此情況下，對 Oracle OCI 函數 Odessp （）的呼叫會失敗，但必須要有才能執行預設參數。 修改基礎資料表許可權之後，必須重新編譯預存程式，然後再執行一次。

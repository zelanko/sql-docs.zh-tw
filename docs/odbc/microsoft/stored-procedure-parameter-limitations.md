---
title: 預存程序參數限制 |Microsoft Docs
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
ms.assetid: 8b804bcf-4cce-4e6f-aa45-00bab9ef9921
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36f1c5a18eb9f0b1939a2c3602f1ebe7695741f7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948821"
---
# <a name="stored-procedure-parameter-limitations"></a>預存程序參數限制
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 當執行 Oracle 預存程序，利用 10 或多個輸出參數時，預存程序呼叫將會失敗，發生存取違規或 ActiveX Data Objects (ADO) 的錯誤所導致。 可能時使用 Microsoft ODBC Driver for Oracle，8.0.4.0.0 和 8.0.4.0.4 Oracle 用戶端軟體版本。  
  
 若要修正這個問題，Oracle 用戶端軟體必須升級為版本 8.0.4.2.0 或更高版本。 如需詳細資訊請連絡 Oracle Corporation[修補程式](../../odbc/microsoft/oracle-software-patches.md)。  
  
> [!NOTE]  
>  早期版本的 Oracle 用戶端軟體版本 8.0.3.0.0 不會發生這個問題。

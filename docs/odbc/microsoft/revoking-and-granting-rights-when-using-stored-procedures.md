---
description: 在使用預存程序時撤銷和授與權限
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
ms.openlocfilehash: ad59f18f040dd1fefec606c99e3cce5f1002c22a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449270"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>在使用預存程序時撤銷和授與權限
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 當授與使用者權限，並在預存程式所存取的資料表上撤銷時，Microsoft ODBC Driver for Oracle 會傳回下列錯誤訊息：  
  
 SQL_ERROR =-1  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 錯誤的參數數目"  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 語法錯誤或存取違規"  
  
 在此案例中，對 Oracle OCI 函式 Odessp ( # A1 的呼叫會失敗，但這是必要的，才能執行預設參數。 修改基礎資料表許可權之後，必須先重新編譯預存程式，再重新執行它。

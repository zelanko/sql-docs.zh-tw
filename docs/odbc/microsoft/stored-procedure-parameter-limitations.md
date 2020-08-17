---
description: 預存程序參數限制
title: 預存程式參數限制 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be3f28c748f1322c3557c1030e2fb79b12db399b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339594"
---
# <a name="stored-procedure-parameter-limitations"></a>預存程序參數限制
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 執行使用10個以上輸出參數的 Oracle 預存程式時，預存程序呼叫會失敗，導致存取違規或 ActiveX Data Objects (ADO) 錯誤。 使用 Microsoft ODBC Driver for Oracle 搭配8.0.4.0.0 和8.0.4.0.4 的 Oracle 用戶端軟體時，就會發生這種情況。  
  
 若要修正此問題，必須將 Oracle 用戶端軟體升級至8.0.4.2.0 版或更高版本。 如需 [修補程式](../../odbc/microsoft/oracle-software-patches.md)的詳細資訊，請洽詢 Oracle Corporation。  
  
> [!NOTE]  
>  早期版本的 Oracle 用戶端軟體版本8.0.3.0.0 不會發生此問題。

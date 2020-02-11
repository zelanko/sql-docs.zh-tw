---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 36f1c5a18eb9f0b1939a2c3602f1ebe7695741f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948821"
---
# <a name="stored-procedure-parameter-limitations"></a>預存程序參數限制
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 執行使用10個或更多輸出參數的 Oracle 預存程式時，預存程序呼叫將會失敗，因而導致發生存取違規或 ActiveX Data Objects （ADO）錯誤。 使用適用于 Oracle 的 Microsoft ODBC 驅動程式搭配 Oracle 用戶端軟體的版本8.0.4.0.0 和8.0.4.0.4 時，可能會發生這種情況。  
  
 若要修正此問題，必須將 Oracle 用戶端軟體升級為8.0.4.2.0 或更高版本。 如需[修補程式](../../odbc/microsoft/oracle-software-patches.md)的詳細資訊，請洽詢 Oracle Corporation。  
  
> [!NOTE]  
>  早期版本的 Oracle 用戶端軟體版本8.0.3.0.0 不會發生此問題。

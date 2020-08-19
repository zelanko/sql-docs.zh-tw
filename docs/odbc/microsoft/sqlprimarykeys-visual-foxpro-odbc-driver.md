---
description: SQLPrimaryKeys (Visual FoxPro ODBC Driver)
title: SQLPrimaryKeys (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96b333e10c7000a8a44e957e33d0c84a3b004f43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483341"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 支援： Full  
  
 ODBC API 一致性：層級2  
  
 傳回組成資料表之主鍵的資料行名稱。 **SQLPrimaryKeys**的 VISUAL FoxPro ODBC 驅動程式執行行為如下：  
  
-   忽略 *szTableOwner* 和 *cbTableOwner* 引數。  
  
-   僅適用于 [資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的資料來源。 如果資料來源是 [可用資料表](../../odbc/microsoft/visual-foxpro-terminology.md)的目錄，驅動程式會傳回錯誤「驅動程式不支援此函式」。  
  
 如需詳細資訊，請參閱《 *ODBC 程式設計人員參考*》中的[SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) 。

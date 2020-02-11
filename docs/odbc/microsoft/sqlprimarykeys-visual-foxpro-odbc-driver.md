---
title: SQLPrimaryKeys （Visual FoxPro ODBC Driver） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e85e60cde86c9483e69a8c43de14ef64eb914119
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68030698"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：層級2  
  
 傳回組成資料表主鍵的資料行名稱。 **SQLPrimaryKeys**的 VISUAL FoxPro ODBC Driver 執行行為如下所示：  
  
-   忽略*szTableOwner*和*cbTableOwner*引數。  
  
-   僅適用于[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的資料來源。 如果資料來源是[可用資料表](../../odbc/microsoft/visual-foxpro-terminology.md)的目錄，驅動程式會傳回「驅動程式不支援此函數」錯誤。  
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) 。

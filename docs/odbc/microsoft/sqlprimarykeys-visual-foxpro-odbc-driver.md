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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83631d22bd07017c4eba8f6af171443ab8c76d9c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301543"
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

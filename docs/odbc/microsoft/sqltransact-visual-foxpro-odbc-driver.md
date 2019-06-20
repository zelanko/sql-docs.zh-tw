---
title: SQLTransact (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1581cb7ecc694dc9adcbb03d83cf73a6ba41dbed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63270036"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支援：完整  
  
 ODBC API 相容性：核心層級  
  
 要求所有的陳述式控制代碼上的所有作用中作業的認可或回復作業 (*hstmt*s) 與連線，或環境控制代碼相關聯的所有連線相關聯*henv*。 **SQLTransact**僅適用於資料來源[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)。  
  
 如果認可失敗，在手動模式中，交易會維持使用中;您可以選擇要回復交易，或重試認可作業。 如果認可作業失敗時在自動的交易模式下，異動會自動回復;交易不可為非作用中。  
  
 如需詳細資訊，請參閱 < [SQLTransact](../../odbc/reference/syntax/sqltransact-function.md)中*ODBC 程式設計人員參考*。

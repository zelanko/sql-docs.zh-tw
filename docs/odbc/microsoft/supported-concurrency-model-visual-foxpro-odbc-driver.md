---
title: 支援並行存取模型 (Visual FoxPro ODBC Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 597d1022fa6946e0ae768cb9600a3f4534c67a25
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080687"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>支援的並行存取模型 (Visual FoxPro ODBC Driver)
Visual FoxPro ODBC 驅動程式支援*唯讀並行*。 您的應用程式可以呼叫[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CONCUR_READ_ONLY SQL_CONCURRENCY 選項。  
  
 如需詳細資訊，請參閱 < [ODBC 程式設計人員參考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="read-only-concurrency"></a>唯讀並行存取  
 無法更新資料指標。  
  
## <a name="row-versioning"></a>資料列版本設定  
 基本上是時間戳記的支援，在哪一個資料列版本比較在更新時間。

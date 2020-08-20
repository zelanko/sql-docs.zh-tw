---
description: 支援的並行存取模型 (Visual FoxPro ODBC Driver)
title: 支援的並行模型 (Visual FoxPro ODBC 驅動程式) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1be0a7e9ea3700941282f23956a8c304a1ef7f5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500101"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>支援的並行存取模型 (Visual FoxPro ODBC Driver)
Visual FoxPro ODBC 驅動程式支援 *唯讀的並行*存取。 您的應用程式可以使用 SQL_CONCUR_READ_ONLY 的 SQL_CONCURRENCY 選項來呼叫 [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) 。  
  
 如需詳細資訊，請參閱《 ODBC 程式設計 [人員參考](../../odbc/reference/odbc-programmer-s-reference.md)》。  
  
## <a name="read-only-concurrency"></a>唯讀平行存取  
 無法更新資料指標。  
  
## <a name="row-versioning"></a>資料列版本設定  
 基本上是時間戳記支援，其中的資料列版本會在更新時進行比較。

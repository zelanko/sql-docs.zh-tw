---
description: 驅動程式
title: 驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC]
- drivers [ODBC], about drivers
ms.assetid: d6795d92-877e-44e1-b7d5-2ff2fd3989bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81e8989fc178728e687baa13b37e6055692d9413
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494591"
---
# <a name="drivers"></a>驅動程式
*驅動程式* 是在 ODBC API 中執行函式的程式庫。 每一個都是特定的 DBMS 所特有;例如，Oracle 的驅動程式無法直接存取 Informix DBMS 中的資料。 驅動程式會公開基礎 Dbms 的功能;它們不需要執行 DBMS 所支援的功能。 例如，如果基礎 DBMS 不支援外部聯結，則這兩個驅動程式都不適用。 唯一的唯一例外是，如果 Dbms 的驅動程式沒有獨立的資料庫引擎（例如 Xbase），則必須執行至少支援最少 SQL 數量的資料庫引擎。  
  
 此章節包含下列主題。  
  
-   [驅動程式工作](../../odbc/reference/driver-tasks.md)  
  
-   [驅動程式架構](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 提供的 ODBC 驅動程式](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)

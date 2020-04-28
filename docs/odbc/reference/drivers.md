---
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
ms.openlocfilehash: 7c8b40641be3db34fc6929edecdd5dd923700957
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294181"
---
# <a name="drivers"></a>驅動程式
*驅動程式*是在 ODBC API 中執行函式的程式庫。 每個都是特定的 DBMS 特有的;例如，Oracle 的驅動程式無法直接存取 Informix DBMS 中的資料。 驅動程式會公開基礎 Dbms 的功能;不需要它們來執行 DBMS 所不支援的功能。 例如，如果基礎 DBMS 不支援外部聯結，驅動程式就不應該這樣做。 唯一的例外是，Dbms 的驅動程式若沒有獨立的資料庫引擎（例如 Xbase），就必須執行至少支援最低 SQL 數量的資料庫引擎。  
  
 此章節包含下列主題。  
  
-   [驅動程式工作](../../odbc/reference/driver-tasks.md)  
  
-   [驅動程式架構](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 提供的 ODBC 驅動程式](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)

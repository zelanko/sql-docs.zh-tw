---
title: 驅動程式 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294181"
---
# <a name="drivers"></a>驅動程式
*驅動程式*是在 ODBC API 中實現函數的庫。 每個都特定於特定的 DBMS;例如,Oracle 的驅動程式不能直接訪問 Informix DBMS 中的數據。 驅動程序公開底層 DBMS 的功能;它們不需要實現 DBMS 不支援的功能。 例如,如果基礎 DBMS 不支援外部聯接,則驅動程式也不應支援外部聯接。 唯一的主要例外是,沒有獨立資料庫引擎(如 Xbase)的 DBMS 的驅動程式必須實現至少支援最少數量的 SQL 的資料庫引擎。  
  
 此章節包含下列主題。  
  
-   [驅動程式工作](../../odbc/reference/driver-tasks.md)  
  
-   [驅動程式架構](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 提供的 ODBC 驅動程式](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)

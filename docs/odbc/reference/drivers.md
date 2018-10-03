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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e3996aafa0e4f5b389e4f46d5df3b22632daad9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47710036"
---
# <a name="drivers"></a>驅動程式
*驅動程式*ODBC API 中實作的函式的程式庫。 每一個都是特定 dbms 所特有;例如，Oracle 的驅動程式無法直接存取中的 Informix DBMS 的資料。 驅動程式會公開基礎 Dbms; 的功能它們不需要實作不支援的 DBMS 的功能。 例如，如果基礎 DBMS 不支援外部聯結中，則不應該驅動程式。 僅重大例外狀況是針對 Dbms 沒有獨立的資料庫引擎、 Xbase，例如驅動程式必須實作至少支援最少量的 SQL 資料庫引擎。  
  
 此章節包含下列主題。  
  
-   [驅動程式工作](../../odbc/reference/driver-tasks.md)  
  
-   [驅動程式架構](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 提供的 ODBC 驅動程式](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)

---
title: 支援原生編譯的預存程序建構 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6cdd5c7d154f1841aa5c90e110a596d8684a535
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233268"
---
# <a name="supported-constructs-on-natively-compiled-stored-procedures"></a>原生編譯的預存程序上支援的建構
  本主題列出原生編譯預存程序所支援的建構。  
  
 如需不受支援建構的相關資訊，請參閱[記憶體中的 OLTP 不支援 Transact-SQL 建構](transact-sql-constructs-not-supported-by-in-memory-oltp.md)。  
  
## <a name="procedure-ddl"></a>程序 DDL  
 支援下列功能：  
  
-   CREATE PROCEDURE  
  
-   DROP PROCEDURE  
  
-   SCHEMABINDING (原生編譯預存程序所需的)  
  
-   NATIVE_COMPILATION  
  
-   參數可以宣告為 NOT NULL。  
  
-   資料表值參數。  
  
## <a name="security"></a>Security  
 支援下列功能：  
  
-   針對程序：EXECUTE AS OWNER、SELF 和使用者。  
  
-   資料表和程序的 GRANT 和 DENY 權限。  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程序](natively-compiled-stored-procedures.md)  
  
  

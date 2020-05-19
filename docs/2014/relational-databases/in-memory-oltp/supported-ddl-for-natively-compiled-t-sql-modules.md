---
title: 原生編譯預存程式上支援的結構 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0c439a424c409522eee696d0161c94251e82fb35
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718821"
---
# <a name="supported-constructs-on-natively-compiled-stored-procedures"></a>原生編譯的預存程序上支援的建構
  本主題列出原生編譯預存程序所支援的建構。  
  
 如需不受支援建構的相關資訊，請參閱 [記憶體中的 OLTP 不支援 Transact-SQL 建構](transact-sql-constructs-not-supported-by-in-memory-oltp.md)。  
  
## <a name="procedure-ddl"></a>程序 DDL  
 支援下列功能：  
  
-   CREATE PROCEDURE  
  
-   DROP PROCEDURE  
  
-   SCHEMABINDING (原生編譯預存程序所需的)  
  
-   NATIVE_COMPILATION  
  
-   參數可以宣告為 NOT NULL。  
  
-   資料表值參數。  
  
## <a name="security"></a>安全性  
 支援下列功能：  
  
-   針對程序：EXECUTE AS OWNER、SELF 和使用者。  
  
-   資料表和程序的 GRANT 和 DENY 權限。  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程式](natively-compiled-stored-procedures.md)  
  
  

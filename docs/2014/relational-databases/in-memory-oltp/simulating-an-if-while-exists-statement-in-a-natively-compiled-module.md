---
title: 在原生編譯的預存程式中模擬 EXISTS 子句 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 892dd145ea19c40bada704387a4b2408e84d9522
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718938"
---
# <a name="simulating-an-exists-clause-in-a-natively-compiled-stored-procedure"></a>在原生編譯預存程序中模擬 EXISTS 子句
  原生編譯預存程序不支援 `EXISTS` 子句，但是有解決方法：  
  
```sql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE ...  
IF @exists = 1  
```  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯預存程式的遷移問題](migration-issues-for-natively-compiled-stored-procedures.md)   
 [記憶體中的 OLTP 不支援 Transact-SQL 建構](transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  

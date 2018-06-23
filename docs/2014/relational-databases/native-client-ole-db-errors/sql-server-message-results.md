---
title: SQL Server 訊息結果 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7d1f6519c927bc8050590c1cc13821a7b7895f8a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033000"
---
# <a name="sql-server-message-results"></a>SQL Server 訊息結果
  下列[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式不會產生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者資料列集或計數受影響的資料列執行時：  
  
-   PRINT  
  
-   具有 10 或更低嚴重性的 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 這些陳述式會傳回一或多個參考用訊息，或使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回參考用訊息來取代資料列集或計數結果。 在成功執行， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者傳回 S_OK，而且訊息可以提供給[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者取用者。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回 S_OK，且具有一個或多個參考用訊息可取得在執行許多[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式或取用者執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者成員函式。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者取用者，允許動態指定查詢文字應該檢查錯誤介面，每個成員函式執行之後的值為何傳回碼、 與否傳回**IRowset**或**IMultipleResults**介面參考或受影響的資料列計數。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](errors.md)  
  
  
---
title: SQL Server 訊息結果 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 577b609fd2f878e6c97010cac004e0b10b3a4e4e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300962"
---
# <a name="sql-server-message-results"></a>SQL Server 訊息結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  執行時[!INCLUDE[tsql](../../includes/tsql-md.md)],以下文句[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會 生成本機客戶端 OLE 資料庫提供者行集或受影響行計數:  
  
-   PRINT  
  
-   具有 10 或更低嚴重性的 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 這些陳述式會傳回一或多個參考用訊息，或使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回參考用訊息來取代資料列集或計數結果。 成功執行後,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式返回S_OK,並且[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]消息可供 本機用戶端 OLE 資料庫提供程式消費者使用。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式返回S_OK[!INCLUDE[tsql](../../includes/tsql-md.md)]並在執行許多 語句或本機用戶端 OLE DB[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供程式成員函數的消費者 執行後提供一個或多個資訊訊息。  
  
 允許[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]查詢文本動態規範的原生用戶端 OLE DB 提供程式應在每個成員函數執行後檢查錯誤介面,而不考慮返回代碼的值、返回的**IRowset**或**IMulti 結果**介面引用的存在或不存在,或受影響的行計數。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  

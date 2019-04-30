---
title: 跨資料庫查詢 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a0305f5b-91bd-4d18-a2fc-ec235b062fd3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d8739a95f0676adfdbc890512aeb5246565bacdb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63071587"
---
# <a name="cross-database-queries"></a>跨資料庫查詢
  在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 中，記憶體最佳化資料表不支援跨資料庫的交易。 您無法在同時存取記憶體最佳化資料表的相同交易或相同查詢中存取另一個資料庫。 您無法輕鬆地從某一個資料庫的資料表中，將資料複製到另一個資料庫中的記憶體最佳化資料表。  
  
 資料表變數並非交易式。 因此，記憶體最佳化資料表變數可以在跨資料庫查詢中使用，也因而有助於將某個資料庫中的資料移至另一個資料庫的記憶體最佳化資料表中。 您可以使用兩筆交易。 在第一筆交易中，將資料從遠端資料表插入變數中。 在第二筆交易中，從變數中將資料插入本機記憶體最佳化資料表。  
  
 例如，若要複製的資料列中，資料庫 db1 中資料表 t1 到 db2 中的資料表 t2 使用變數@v1的型別 dbo.tt1，您可以使用類似：  
  
```sql  
USE db2   
GO   
DECLARE @v1 dbo.tt1   
INSERT @v1 SELECT * FROM db1.dbo.t1   
INSERT dbo.t2 SELECT * FROM @v1   
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](migrating-to-in-memory-oltp.md)  
  
  

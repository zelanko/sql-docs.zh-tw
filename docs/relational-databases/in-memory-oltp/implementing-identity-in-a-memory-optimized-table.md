---
title: "在記憶體最佳化資料表中實作 IDENTITY | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 21133ec5172c13b5d010c9aef1f461282acd35b5
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>在記憶體最佳化資料表中實作 IDENTITY
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

只要種子和遞增值皆為 1 (預設值)，記憶體最佳化資料表便支援 IDENTITY。 記憶體最佳化資料表不支援定義為 IDENTITY(x, y) (其中 x != 1 或 y != 1) 的識別欄位。   
    
若要增加 IDENTITY 種子，請使用工作階段選項 `SET IDENTITY_INSERT table_name ON`，插入具有識別欄位之明確值的新資料列。 插入資料列之後，IDENTITY 種子會變更為明確插入的值加上 1。 例如，若要將種子增加到 1000，請插入識別欄位值為 999 的資料列。 產生的識別值接著會從 1000 開始。     
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  


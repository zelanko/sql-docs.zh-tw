---
title: 移除在 DML 觸發程序的 inserted 及 deleted 資料表的 DDL 作業 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- data definition language [SQL Server]
- DDL statements [SQL Server]
- DML triggers, removing DDL operations
ms.assetid: e49ba7d5-787f-4052-b985-b699195d982b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1113b0dd823c2479cff950233d0811f6c017afc9
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582051"
---
# <a name="remove-ddl-operations-on-the-inserted-and-deleted-tables-inside-dml-triggers"></a>在 DML 觸發程序內，移除已插入和已刪除資料表的 DDL 作業
  資料定義語言 (DDL) 陳述式，例如建立索引，無法在 DML 觸發程序的 inserted 及 deleted 資料表上執行。 在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，您可以在插入和刪除的資料表上執行某些 DDL 陳述式。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜使用插入和刪除的資料表＞。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 請移除在 DML 觸發程序內部所插入和刪除之資料表上執行的任何 DDL 作業。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  

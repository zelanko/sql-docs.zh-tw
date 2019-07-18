---
title: 在 90 或之後的相容性模式中包含 TOP 的檢視中不會支援 WITH CHECK OPTION |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- TOP clause
- WITH CHECK OPTION clause
ms.assetid: 1b9581d0-bad9-43e0-b8fc-f32d8a8a04ca
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 254969e6201795e2f4ae512e03be26419b71d866
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090995"
---
# <a name="with-check-option-is-not-supported-in-views-that-contain-top-in-90-or-later-compatibility-modes"></a>在 90 或之後的相容性模式中，在包含 TOP 的檢視中不支援 WITH CHECK OPTION
  Upgrade Advisor 偵測到有檢視在該檢視的 SELECT 陳述式中或它所參考的檢視中使用 WITH CHECK OPTION 和 TOP 子句。 當資料庫相容性模式設定為 80 及之前的相容性模式時，以此方式定義的檢視會錯誤地允許資料透過檢視修改，而產生不正確的結果。 當檢視或它所參考的檢視使用 TOP 子句，而且資料庫相容性模式設定為 90 或之後的相容性模式時，資料無法透過使用 WITH CHECK OPTION 的檢視進行插入或更新。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 當您升級時，使用者資料庫會維持其相容性模式。 在您將資料庫相容性模式變更為 100 或之後以前，如果需要透過檢視進行資料修改，請修改使用 WITH CHECK OPTION 和 TOP 的檢視。 如需詳細資訊，請參閱 < [sp_dbcmptlevel &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbcmptlevel-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  

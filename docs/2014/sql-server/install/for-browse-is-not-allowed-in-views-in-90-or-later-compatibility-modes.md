---
title: 在 90 或之後的相容性模式中的檢視中不允許瀏覽的 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- views [SQL Server], FOR BROWSE clause
- FOR BROWSE clause
ms.assetid: 8f49b1c1-d877-4c46-b988-f8cdd8ac0925
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 87a937dafea15fdc9eca3bbbafbacc17275374b1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037148"
---
# <a name="for-browse-is-not-allowed-in-views-in-90-or-later-compatibility-modes"></a>在 90 或 90 之後的相容性模式中，檢視內不允許有 FOR BROWSE
  Upgrade Advisor 偵測到在檢視中使用 FOR BROWSE 子句。 當資料庫相容性模式設定為 80 時，檢視中允許有 FOR BROWSE 子句 (並且會忽略)。 當資料庫相容性模式設定為 90 或之後時，檢視中就不允許有 FOR BROWSE 子句。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 當您升級時，使用者資料庫會維持其相容性模式。 將資料庫相容性模式變更為 90 或之後以前，請從檢視定義中移除 FOR BROWSE 子句。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_dbcmptlevel＞。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  

---
title: 瀏覽不允許在 90 或之後的相容性模式中的檢視 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], FOR BROWSE clause
- FOR BROWSE clause
ms.assetid: 8f49b1c1-d877-4c46-b988-f8cdd8ac0925
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ccd82fd7b971c97319daa480ba3f9a222d026280
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48065508"
---
# <a name="for-browse-is-not-allowed-in-views-in-90-or-later-compatibility-modes"></a>在 90 或 90 之後的相容性模式中，檢視內不允許有 FOR BROWSE
  Upgrade Advisor 偵測到在檢視中使用 FOR BROWSE 子句。 當資料庫相容性模式設定為 80 時，檢視中允許有 FOR BROWSE 子句 (並且會忽略)。 當資料庫相容性模式設定為 90 或之後時，檢視中就不允許有 FOR BROWSE 子句。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 當您升級時，使用者資料庫會維持其相容性模式。 將資料庫相容性模式變更為 90 或之後以前，請從檢視定義中移除 FOR BROWSE 子句。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_dbcmptlevel＞。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  

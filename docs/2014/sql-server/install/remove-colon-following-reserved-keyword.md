---
title: 移除分號下列保留的關鍵字 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- reserved keywords
ms.assetid: 4f23f7e4-7b4d-4e19-86c9-7527bb8b107d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6f68a641caf21e6cc1dfdefbcb31ff78a1fd8aa6
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583031"
---
# <a name="remove-colon-following-reserved-keyword"></a>移除保留關鍵字後面的冒號
  Upgrade Advisor 偵測到指令碼中的保留關鍵字後面有冒號 (:)。 在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，會忽略此語法且成功地執行該陳述式。 現在，當資料庫相容性模式設定為 100 或之後時，此語法會導致陳述式失敗。  
  
 使用者資料庫會維持其相容性模式。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 在您將資料庫相容性模式變更為 100 或之後以前，請移除保留關鍵字後面的冒號，藉以修改指令碼。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_dbcmptlevel＞。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  

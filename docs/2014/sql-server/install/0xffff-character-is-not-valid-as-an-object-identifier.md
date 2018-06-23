---
title: 0xFFFF 字元不是有效的物件識別碼 |Microsoft 文件
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
- 0xFFFF character [SQL Server]
ms.assetid: b2c9c8cf-9194-45e0-be6b-2d5ec52e8153
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ded2cd54bced9ae69e207a1b609688c2fcf3b633
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036931"
---
# <a name="0xffff-character-is-not-valid-as-an-object-identifier"></a>0xFFFF 字元不是有效的物件識別碼
  Upgrade Advisor 在物件識別碼中偵測到 0xFFFF 字元。 當資料庫相容性模式設定為 90 或之後時，[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本無法參考或重新命名識別碼中包含此字元的物件 (例如資料庫、資料表或資料行)。 當您升級為 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 時，使用者資料庫會維持其相容性模式。 將資料庫相容性模式變更為 90 或之後以前，請重新命名包含 0xFFFF 字元的物件。  
  
 如需有關識別碼的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜識別碼＞。 如需有關資料庫相容性模式的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_dbcmptlevel＞。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  

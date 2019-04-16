---
title: 0xFFFF 字元不是有效的物件識別碼 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- 0xFFFF character [SQL Server]
ms.assetid: b2c9c8cf-9194-45e0-be6b-2d5ec52e8153
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b41d10fde129319c14fe5a5409391cb1abd6f826
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582169"
---
# <a name="0xffff-character-is-not-valid-as-an-object-identifier"></a>0xFFFF 字元不是有效的物件識別碼
  Upgrade Advisor 在物件識別碼中偵測到 0xFFFF 字元。 當資料庫相容性模式設定為 90 或之後時，[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本無法參考或重新命名識別碼中包含此字元的物件 (例如資料庫、資料表或資料行)。 當您升級為 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 時，使用者資料庫會維持其相容性模式。 將資料庫相容性模式變更為 90 或之後以前，請重新命名包含 0xFFFF 字元的物件。  
  
 如需有關識別碼的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜識別碼＞。 如需有關資料庫相容性模式的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜sp_dbcmptlevel＞。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  

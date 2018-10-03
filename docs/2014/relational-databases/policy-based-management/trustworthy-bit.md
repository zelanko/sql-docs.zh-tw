---
title: Trustworthy 位元 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3198188a-2b59-4865-9560-10f760934b8e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 524c1c330288579649fd7744366cf8f3866fe8a6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072108"
---
# <a name="trustworthy-bit"></a>Trustworthy 位元
  此規則會判斷資料庫的 dbo 角色是否指派給系統管理員 (sysadmin) 固定伺服器角色，且資料庫的 trustworthy 位元是否設定為 ON。  
  
 如果滿足這些條件，有權限的資料庫使用者可以將權限提高為系統管理員 (sysadmin) 角色。 在這個角色中，使用者可以建立及執行危害系統的不安全組件。  
  
## <a name="best-practices-recommendations"></a>最佳做法建議  
 關閉 trustworthy 位元，或是從 dbo 資料庫角色撤銷系統管理員 (sysadmin) 權限。  
  
## <a name="for-more-information"></a>詳細資訊  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
## <a name="see-also"></a>另請參閱  
 [使用原則式管理來監視和強制最佳做法](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  

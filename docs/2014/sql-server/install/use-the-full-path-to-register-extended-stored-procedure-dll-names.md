---
title: 使用完整路徑，註冊擴充預存程序 DLL 名稱 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- registering DLL names
- extended stored procedures [SQL Server], registering
- DLL names [SQL Server]
- full path DLL name registration [SQL Server]
ms.assetid: f648d57c-af32-4c71-9882-47b6766f3c2b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2ecdf37d4c7c97e8c474f5e7f08e3e6fef040723
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62689785"
---
# <a name="use-the-full-path-to-register-extended-stored-procedure-dll-names"></a>使用完整路徑，註冊擴充預存程序 DLL 名稱
  先前未使用完整路徑註冊 DLL 名稱的擴充預存程序，可能無法在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中運作。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 先前未使用完整路徑註冊 DLL 名稱的擴充預存程序，在升級之後可能無法運作。 這是因為在升級程序期間，舊的 BINN 目錄不會加入至新路徑。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能找不到擴充預存程序。  
  
## <a name="corrective-action"></a>更正動作  
 升級之前，請針對未使用完整路徑名稱註冊的每個擴充預存程序遵循下列步驟進行：  
  
1.  執行 sp_dropextendedproc，以便移除擴充預存程序。  
  
2.  執行 sp_addextendedproc，以便使用完整路徑名稱來註冊擴充預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  

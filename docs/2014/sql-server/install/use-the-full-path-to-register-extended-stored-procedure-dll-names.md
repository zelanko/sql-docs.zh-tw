---
title: 使用完整路徑來註冊擴充預存程式 DLL 名稱 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
ms.openlocfilehash: e560ec0fd617d4da46235803da8cbd69ef4f80d5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091293"
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
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  

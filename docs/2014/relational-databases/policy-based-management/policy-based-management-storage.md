---
title: 原則式管理原則儲存 | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b741f03de6a1c36678752b1d0f926479dec91c0b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032989"
---
# <a name="policy-based-management-storage"></a>原則式管理原則儲存
  原則會儲存在 msdb 資料庫中。 變更原則或條件之後，就應該備份 msdb。 如需詳細資訊，請參閱[系統資料庫的備份與還原 &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)。  
  
## <a name="storing-policies"></a>儲存原則  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 包含一些可用來監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的原則。 根據預設，這些原則不會安裝在[!INCLUDE[ssDE](../../includes/ssde-md.md)]; 不過，您可以從 C:\Program Files (x86) \Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033 的預設安裝位置匯入。  
  
 您可以使用 [檔案/新增] 功能表來直接建立原則，然後將它們儲存至檔案。 當您沒有連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體時，這樣就可讓您建立原則。  
  
 在目前 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體中評估之原則的原則記錄會保存在 msdb 系統資料表中。 套用至其他 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體或套用至 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 之原則的原則記錄則不會保留。  
  
  
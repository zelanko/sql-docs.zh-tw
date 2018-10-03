---
title: SQL Server 2005 中，SERVERPROPERTY 會傳回 LCID 屬性的正確結果 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SERVERPROPERTY function
ms.assetid: 833a2fc9-b480-4697-aa7b-9677e78ee0b4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a05202e19e95e719c8518f785be7ee1a1fbd8fff
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48163098"
---
# <a name="serverproperty-returns-correct-result-for-lcid-property-in-sql-server-2005"></a>在 SQL Server 2005 中，SERVERPROPERTY 會傳回 LCID 屬性的正確結果
  如果 SERVERPROPERTY('LCID') 是在二進位定序伺服器上執行，則此函數會傳回對應於伺服器定序的 Windows 地區設定識別碼 (LCID)。  
  
> [!NOTE]  
>  對於包含 SERVERPROPERTY ('LCID') 的參考且在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之其他執行個體上執行的批次和追蹤檔案，只有在其他執行個體具有與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之目前執行個體相同的定序時，Upgrade Advisor 才會偵測此行為變更。  
  
## <a name="corrective-action"></a>更正動作  
 請修改應用程式以預期 SERVERPROPERTY('LCID') 會傳回對應至伺服器定序的 Windows LCID。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  

---
title: 修改應用程式以接受來自 sysperfinfo.cntr_value 的 bigint 值 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- sysperfinfo
- bigint values [SQL Server]
ms.assetid: b0345303-6e9a-4078-8148-6e1bce207b8c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 835e5fae4717748664affef9491ea1f7eeaec8b2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199921"
---
# <a name="modify-applications-to-expect-bigint-values-from-sysperfinfocntrvalue"></a>修改應用程式以接受來自 sysperfinfo.cntr_value 的 bigint 值
  sysperfinfo 會傳回`bigint`cntr_value 資料行的值。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>更正動作  
 請修改使用 sysperfinfo 的應用程式，以確保它們能夠處理 cntr_value 資料行的 `bigint` 值。  
  
> [!NOTE]  
>  sysperfinfo 是相容性檢視。 您應該改用 sys.dm_os_performance_counter 動態管理檢視。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](sql-server-2014-upgrade-advisor.md)  
  
  

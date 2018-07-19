---
title: INFORMATION_SCHEMA。執行個體中的結構描述傳回結構描述名稱，在資料庫中，不資料庫 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
ms.assetid: 4337b643-910d-47d7-bea8-f4052066b9a2
caps.latest.revision: 19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c32683c6dc6aaa26079443d2ff4bc5d1f0994d76
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198438"
---
# <a name="informationschemaschemata-returns-schema-names-in-a-database-not-databases-in-an-instance"></a>INFORMATION_SCHEMA.SCHEMATA 會傳回資料庫 (非執行個體中的資料庫) 中的結構描述名稱
  Upgrade Advisor 偵測到參考 INFORMATION_SCHEMA.SCHEMATA 檢視的陳述式。 在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，此檢視會傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的所有資料庫。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本中，此檢視會傳回資料庫中的所有結構描述。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，INFORMATION_SCHEMA.SCHEMATA 檢視會傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的所有資料庫。 現在，該檢視會傳回符合「SQL 標準」之資料庫中的所有結構描述。  
  
## <a name="corrective-action"></a>更正動作  
 修改您的應用程式參考**sys.databases**目錄檢視，以傳回所有資料庫的執行個體中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新增&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  

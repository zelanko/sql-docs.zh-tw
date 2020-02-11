---
title: 移除卸載系統物件的語句 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1d420e2dba1dfdb284b0002eca6d8408c4e019e8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093080"
---
# <a name="remove-statements-that-drop-system-objects"></a>移除卸除系統物件的陳述式
  Upgrade Advisor 偵測到卸除系統物件的陳述式。 系統物件（包含擴充預存程式）會部署在唯讀的**resource**資料庫（mssqlsystemresource）中，而且無法卸載。 請修改您的應用程式，以便撤銷或拒絕系統物件的 EXECUTE 權限。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 DROP TABLE、DROP PROCEDURE 和**sp_dropextendedproc**之類的語句無法用來移除系統物件，因為這些物件是部署在唯讀的**resource**資料庫中。  
  
## <a name="corrective-action"></a>更正動作  
 請移除嘗試從應用程式中卸除系統物件的所有陳述式。 請修改您的應用程式，以便撤銷或拒絕系統物件的 EXECUTE 權限。 或者，您也可以使用介面區組態 (SAC) 工具來停用其中某些物件。 例如，您可以使用 SAC 工具來停用或啟用**xp_cmdshell**擴充預存程式。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎升級問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新的&#93;](sql-server-2014-upgrade-advisor.md)  
  
  

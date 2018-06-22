---
title: SQL Server Reporting Services Standard 和 Enterprise 的 CPU 和記憶體限制變更 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dd553715-2b95-4119-8f58-d01de388d9ab
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5097398d50c2e3072c31724cd16e56d63f5e7676
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023503"
---
# <a name="changes-to-cpu-and-memory-limits-for-sql-server-reporting-services-standard-and-enterprise"></a>SQL Server Reporting Services Standard 和 Enterprise 之 CPU 和記憶體限制的變更
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services Standard 和 Enterprise 最多可支援 64 GB 的系統記憶體。  
  
## <a name="component"></a>元件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
### <a name="description"></a>描述  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services Standard 和 Enterprise 最多可支援 64 GB 的系統記憶體。 您可能需要重新設定目前的系統設定，才能符合新的限制。  
  
 如需有關針對其他版本的 CPU 和記憶體限制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱[Compute Capacity Limits by Edition of SQL Server](../compute-capacity-limits-by-edition-of-sql-server.md)，和[支援 SQL Server 版本的記憶體](http://go.microsoft.com/fwlink/?LinkId=212633)。  
  
## <a name="corrective-action"></a>更正動作  
 您可能需要重新設定目前的系統設定，才能符合新的 CPU 和記憶體限制。 如需詳細資訊，請參閱[ALTER SERVER CONFIGURATION &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)，和[伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 各版本所支援的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [回溯相容性](../../../2014/getting-started/backward-compatibility.md)  
  
  

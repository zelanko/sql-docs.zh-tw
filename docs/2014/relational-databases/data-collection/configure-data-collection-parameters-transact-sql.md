---
title: 設定資料收集參數 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collection [SQL Server]
ms.assetid: 850905b6-35d2-4ed1-ab51-de64daa832b2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 51e0b8360c0b5aa6662fb317a62d7ce52bf4fc41
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748900"
---
# <a name="configure-data-collection-parameters-transact-sql"></a>設定資料收集參數 (Transact-SQL)
  在您建立自訂收集組之前，必須先設定資料收集參數。 您可以使用資料收集器所提供的預存程序來完成此作業。 完成這項工作需要在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用查詢編輯器來進行以下程序。  
  
> [!NOTE]  
>  只設定資料收集參數一次。 在組態設定之後，這些參數會用於您所建立的其他任何收集組。  
  
### <a name="configure-data-collection-parameters"></a>設定資料收集參數  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接到您想要建立自訂收集組的資料庫。  
  
2.  在查詢編輯器中，發出下列陳述式。  
  
    ```tsql  
    USE msdb;  
    EXEC sp_syscollector_set_warehouse_instance_name N'INSTANCE_NAME';-- where instance name is the name of the SQL Server instance  
    EXEC sp_syscollector_set_warehouse_database_name N'MDW';  
    EXEC sp_syscollector_set_cache_directory N'D:\tempdata';  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [資料收集](data-collection.md)   
 [資料收集器預存程序 &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql)  
  
  

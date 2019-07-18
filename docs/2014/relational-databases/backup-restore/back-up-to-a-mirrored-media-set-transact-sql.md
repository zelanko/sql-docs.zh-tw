---
title: 備份至鏡像媒體集 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 5fc43a5d-dfd6-4c53-a4ef-3c8da23ccc81
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 88ea15fabe8e8fd6630d3430417879c7104dff67
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62876947"
---
# <a name="back-up-to-a-mirrored-media-set-transact-sql"></a>備份至鏡像媒體集 (Transact-SQL)
  此主題描述在備份 [!INCLUDE[tsql](../../includes/tsql-md.md)][資料庫時，如何使用](/sql/t-sql/statements/backup-transact-sql) BACKUP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式來指定鏡像媒體集。 請在 BACKUP 陳述式中，指定 TO 子句中的第一個鏡像。 然後在鏡像自身的 MIRROR TO 子句中指定每一個鏡像。 TO 和 MIRROR TO 子句都必須指定相同的備份裝置數目和類型。  
  
## <a name="example"></a>範例  
 下列範例會建立先前圖表中所闡述的鏡像媒體集，並將 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫備份至兩個鏡像。  
  
```  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
    FORMAT,  
    MEDIANAME = 'AdventureWorks2012Set1';  
GO  
```  
  
## <a name="related-tasks"></a>相關工作  
 **從鏡像備份還原**  
  
-   [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [鏡像備份媒體集 &#40;SQL Server&#41;](mirrored-backup-media-sets-sql-server.md)  
  
  

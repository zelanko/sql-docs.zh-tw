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
ms.openlocfilehash: 255a3c190139c029f5211dcab9780b6d07d975a4
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84959488"
---
# <a name="back-up-to-a-mirrored-media-set-transact-sql"></a>備份至鏡像媒體集 (Transact-SQL)
  本主題描述在備份資料庫時，如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](/sql/t-sql/statements/backup-transact-sql)語句來指定鏡像媒體集 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 請在 BACKUP 陳述式中，指定 TO 子句中的第一個鏡像。 然後在鏡像自身的 MIRROR TO 子句中指定每一個鏡像。 TO 和 MIRROR TO 子句都必須指定相同的備份裝置數目和類型。  
  
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
  
  

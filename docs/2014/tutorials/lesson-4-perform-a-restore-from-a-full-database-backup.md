---
title: 第 4 課： 從完整資料庫備份執行還原 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 580f76e6-9802-4abc-9043-db6de592c733
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8869fa4bba6050dd0c15b8b59b7f2d091902936f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022793"
---
# <a name="lesson-4-perform-a-restore-from-a-full-database-backup"></a>第 4 課：從完整資料庫備份執行還原
  這一課將示範如何使用 tsql 陳述式，從上一課建立的完整資料庫備份執行還原。  
  
## <a name="perform-a-restore-of-a-database-backup"></a>執行資料庫備份的還原  
 若要還原完整資料庫備份，請使用下列步驟：  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]。  
  
2.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]的執行個體。  
  
3.  在 [標準] 功能表列上，按一下 **[新增查詢]**。  
  
4.  將下列範例複製並貼入查詢視窗中，並視需要修改。  
  
    ```  
    RESTORE DATABASE AdventureWorks2012   
    FROM URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    WITH CREDENTIAL = 'mycredential';  
    , STATS = 5 – use this to see monitor the progress  
    GO  
  
    ```  
  
5.  確認 T-SQL 陳述式並按一下  **Execute**  
  
### <a name="return-to-tutorials-portal"></a>返回教學課程入口網站  
 [教學課程： SQL Server 備份及還原至 Windows Azure Blob 儲存體服務](../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)。  
  
  
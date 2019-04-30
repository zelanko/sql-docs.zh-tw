---
title: 第 4 課：從完整資料庫備份執行還原 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 580f76e6-9802-4abc-9043-db6de592c733
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 077fb708f09db0182bc5f1510f0264b139beab13
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312065"
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
    , STATS = 5 - use this to see monitor the progress  
    GO  
  
    ```  
  
5.  確認 T-SQL 陳述式，然後按一下**Execute**  
  
### <a name="return-to-tutorials-portal"></a>返回教學課程入口網站  
 [教學課程：SQL Server 備份及還原至 Windows Azure Blob 儲存體服務](../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)。  
  
  

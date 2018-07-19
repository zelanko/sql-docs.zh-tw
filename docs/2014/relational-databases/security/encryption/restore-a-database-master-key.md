---
title: 還原資料庫主要金鑰 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], importing
ms.assetid: 16897cc5-db8f-43bb-a38e-6855c82647cf
caps.latest.revision: 14
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 4720e5faecfb6edac141510aefe389b4d17c3bc8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37307448"
---
# <a name="restore-a-database-master-key"></a>還原資料庫主要金鑰
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ，還原 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中的資料庫主要金鑰。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   [若要使用 Transact-SQL 還原資料庫主要金鑰](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   當主要金鑰還原時， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會解密所有利用目前作用中主要金鑰加密的金鑰，然後利用還原的主要金鑰加密這些金鑰。 這項需要大量資源的作業應該安排在低需求時進行。 如果目前資料庫主要金鑰未開啟或無法開啟，或者，如果利用該金鑰加密的任何金鑰無法解密，還原作業便會失敗。  
  
-   如果任何一項解密失敗，還原便會失敗。 您可以利用 FORCE 選項來省略錯誤，但這個選項會使所有無法解密的資料遺失。  
  
-   如果先前是由服務主要金鑰加密主要金鑰，則還原的主要金鑰也會由服務主要金鑰來加密。  
  
-   如果目前資料庫中沒有主要金鑰，RESTORE MASTER KEY 會建立主要金鑰。 不會自動利用服務主要金鑰來加密新的主要金鑰。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要資料庫的 CONTROL 權限。  
  
##  <a name="SSMSProcedure"></a> 搭配 Transact-SQL 使用 SQL Server Management Studio  
  
#### <a name="to-restore-the-database-master-key"></a>若要還原資料庫主要金鑰  
  
1.  從實體備份媒體或本機檔案系統上的目錄，擷取已備份的資料庫主要金鑰副本。  
  
2.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
3.  在標準列上，按一下 **[新增查詢]**。  
  
4.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- Restores the database master key of the AdventureWorks2012 database.  
    USE AdventureWorks2012;  
    GO  
    RESTORE MASTER KEY   
        FROM FILE = 'c:\backups\keys\AdventureWorks2012_master_key'   
        DECRYPTION BY PASSWORD = '3dH85Hhk003#GHkf02597gheij04'   
        ENCRYPTION BY PASSWORD = '259087M#MyjkFkjhywiyedfgGDFD';  
    GO  
    ```  
  
    > [!NOTE]  
    >  金鑰的檔案路徑和金鑰的密碼 (如果有) 不同於上方指示。 請確定兩者都是您伺服器和金鑰設定專用的。  
  
 如需詳細資訊，請參閱 [RESTORE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-master-key-transact-sql)  
  
  

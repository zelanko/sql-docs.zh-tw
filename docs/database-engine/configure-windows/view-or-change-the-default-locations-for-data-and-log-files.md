---
title: "檢視或變更資料及記錄檔的預設位置 | Microsoft Docs"
ms.custom: 
ms.date: 06/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- log files [SQL Server], changing default location
- data files [SQL Server], changing default location
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
caps.latest.revision: "16"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2f5d4d317ce451cd9080142589817118653a7019
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="view-or-change-the-default-locations-for-data-and-log-files"></a>檢視或變更資料及記錄檔的預設位置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
 保護資料檔和記錄檔的最佳作法是確定它們受到存取控制清單 (ACL) 所保護。 在建立這些檔案的根目錄下設定 ACL。  
 
  
## <a name="view-or-change-the-default-locations-for-database-files"></a>檢視或變更資料庫檔案的預設位置  
  
1.  在物件總管中，以滑鼠右鍵按一下伺服器，然後按一下 [屬性]。  
  
2.  在該 [屬性] 頁面的左面板中，按一下 [資料庫設定] 索引標籤。  
  
3.  在 **[資料庫預設位置]**中，您可以檢視新資料檔和新記錄檔的目前預設位置。 若要變更預設位置，在 **[資料]** 或 **[記錄]** 欄位中輸入新的預設路徑名稱，或按一下 [瀏覽] 按鈕來尋找並選取路徑名稱。  
  
>**注意：** 變更預設位置之後，您必須停止並啟動 SQL Server 服務，才能完成變更。  
  
## <a name="see-also"></a>另請參閱  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [建立資料庫](../../relational-databases/databases/create-a-database.md)  
  
  

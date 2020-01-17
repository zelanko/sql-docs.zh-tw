---
title: 訂閱驗證選項對話方塊 (交易式)
description: 說明 SQL Server Management Studio (SSMS) 中異動複寫的 [訂閱驗證選項] 對話方塊。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.options.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: fd66ad1f-df01-4240-9e89-8f41bff12c1e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 2cf652d154c3e26fecc05c4313c119e6350de330
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2019
ms.locfileid: "75322161"
---
# <a name="subscription-validation-options-transactional-subscriptions"></a>訂閱驗證選項 (交易式訂閱)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  使用 **[訂閱驗證選項]** 對話方塊來指定驗證應該只使用資料列計數，或使用資料列計數與二進位總和檢查碼。 

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>選項。  
 **確認訂閱者與發行者的複寫資料列數相同。**  
 選取要執行之資料列計數驗證的類型。 對於 Oracle 發行集，唯一可用的選項是 **[直接查詢資料表來計算實際資料列計數]** 。  
  
 **比較總和檢查碼來確認資料列資料**  
 除了統計「發行者」與「訂閱者」上的資料列數量之外，也會使用二進位總和檢查碼演算法計算所有資料的總和檢查碼。 如果資料列計數失敗，就不會執行總和檢查碼。  
  
 **完成驗證之後停止散發代理程式。**  
 依預設，散發代理程式會持續執行。 選取此選項即可在執行驗證之後停止代理程式。 此選項可以讓您在繼續複寫資料至訂閱者之前，先檢查驗證是否已成功。  
  
## <a name="see-also"></a>另請參閱  
 [驗證訂閱者端的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [驗證複寫的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  

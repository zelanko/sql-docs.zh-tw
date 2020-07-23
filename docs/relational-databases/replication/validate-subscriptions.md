---
title: 驗證多個訂閱 | Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.subscriptions.f1
helpviewer_keywords:
- Validate Subscriptions dialog box
ms.assetid: 0ca39a35-f22c-46c5-82a4-342e34bf5d1b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 8cdff5889849596c0e83d84daf3c7fae73fd4f41
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86920354"
---
# <a name="validate-subscriptions"></a>驗證多個訂閱
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  使用 **[驗證訂閱]** 對話方塊即可指定交易式發行集的訂閱，需要在訂閱的散發代理程式下次執行時進行驗證。 驗證的結果會在複寫監視器中顯示。 如需詳細資訊，請參閱 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>選項。  
 **驗證所有的 SQL Server 訂閱**  
 選取即可驗證此發行集之所有 SQL Server 訂閱的資料。  
  
 **驗證下列訂閱**  
 如果您不要驗證所有訂閱，請進行選取。 從清單中選取您要驗證的訂閱。  
  
 **驗證選項**  
 按一下以存取 **[訂閱驗證選項]** 對話方塊，其中可讓您指定是否要使用資料列計數驗證或二進位總和檢查碼驗證。  
  
## <a name="see-also"></a>另請參閱  
 [驗證複寫的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  

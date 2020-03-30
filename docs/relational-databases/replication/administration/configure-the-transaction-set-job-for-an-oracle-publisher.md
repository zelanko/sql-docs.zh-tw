---
title: 設定交易集作業 (Oracle 發行者)
description: 了解如何針對發行至 SQL Server 訂閱者的 Oracle 發行者設定交易集作業。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_publisherproperty
- Oracle publishing [SQL Server replication], configuring
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8f25f3d9c9a69d3a8f87e8a4eb1886f31092940f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "75322048"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher"></a>設定 Oracle 發行者的交易集作業
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Xactset** 作業是由在「Oracle 發行者」端執行的複寫所建立的 Oracle 資料庫作業，可在「記錄讀取器代理程式」未與「發行者」連接時建立交易集。 您可以使用複寫預存程序，以程式設計的方式從「散發者」啟用和設定此作業。 如需詳細資訊，請參閱 [Oracle 發行者的效能微調](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)。  
  
### <a name="to-enable-the-transaction-set-job"></a>若要啟用交易集作業  
  
1.  在「Oracle 發行者」端，將 **job_queue_processes** 初始化參數設定為足夠的值，以允許 Xactset 作業執行。 如需有關此參數的詳細資訊，請參閱「Oracle 發行者」的資料庫文件。  
  
2.  在「散發者」端執行 [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 針對 **\@publisher** 指定 Oracle 發行者名稱、針對  propertyname **指定 \@xactsetbatching** 值，並針對  propertyvalue **指定 \@enabled** 值。  
  
3.  在「散發者」端執行 [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 針對 **\@publisher** 指定 Oracle 發行者名稱、針對  propertyname **指定 \@xactsetjobinterval** 值，並針對 **\@propertyvalue** 指定作業間隔 (以分鐘計)。  
  
4.  在「散發者」端執行 [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 針對 **\@publisher** 指定 Oracle 發行者名稱、針對  propertyname **指定 \@xactsetjob** 值，並針對  propertyvalue **指定 \@enabled** 值。  
  
### <a name="to-configure-the-transaction-set-job"></a>若要設定交易集作業  
  
1.  (選擇性) 在「散發者」端執行 [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 針對 **\@publisher** 指定 Oracle 發行者的名稱。 這麼做會傳回「發行者」端 **Xactset** 作業的屬性。  
  
2.  在「散發者」端執行 [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 針對 **\@publisher** 指定 Oracle 發行者名稱、針對 **\@propertyname** 指定要設定的 Xactset 作業屬性名稱，並針對 **\@propertyvalue** 指定新設定。  
  
3.  (選擇性) 針對每個要設定的 Xactset 作業屬性重複步驟 2。 在變更 **xactsetjobinterval** 屬性時，您必須在「Oracle 發行者」上重新啟動作業，新的間隔才會生效。  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>若要檢視交易集作業的屬性  
  
1.  在「散發者」端執行 [sp_helpxactsetjob](../../../relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql.md)。 針對 **\@publisher** 指定 Oracle 發行者的名稱。  
  
### <a name="to-disable-the-transaction-set-job"></a>若要停用交易集作業  
  
1.  在「散發者」端執行 [sp_publisherproperty &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md)。 針對 **\@publisher** 指定 Oracle 發行者名稱、針對  propertyname **指定 \@xactsetjob** 值，並針對  propertyvalue **指定 \@disabled** 值。  
  
## <a name="example"></a>範例  
 下列範例會啟用 `Xactset` 作業，並在執行之間設定三分鐘的間隔。  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../relational-databases/replication/codesnippet/tsql/configure-the-transactio_1.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [Oracle 發行者的效能微調](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  

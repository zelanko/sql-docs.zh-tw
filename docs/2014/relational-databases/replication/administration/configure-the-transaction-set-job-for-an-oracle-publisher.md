---
title: 設定 Oracle 發行者 （複寫 TRANSACT-SQL 程式設計） 的交易集作業 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- sp_publisherproperty
- Oracle publishing [SQL Server replication], configuring
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c16d9dbd07be6b66a81e1e9e4f9745b80dccfc0e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022846"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher-replication-transact-sql-programming"></a>設定 Oracle 發行者的交易集作業 (複寫 Transact-SQL 程式設計)
  **Xactset** 作業是由在「Oracle 發行者」端執行的複寫所建立的 Oracle 資料庫作業，可在「記錄讀取器代理程式」未與「發行者」連接時建立交易集。 您可以使用複寫預存程序，以程式設計的方式從「散發者」啟用和設定此作業。 如需詳細資訊，請參閱 [Oracle 發行者的效能微調](../non-sql/performance-tuning-for-oracle-publishers.md)。  
  
### <a name="to-enable-the-transaction-set-job"></a>若要啟用交易集作業  
  
1.  在「Oracle 發行者」端，將 **job_queue_processes** 初始化參數設定為足夠的值，以允許 Xactset 作業執行。 如需有關此參數的詳細資訊，請參閱「Oracle 發行者」的資料庫文件。  
  
2.  在「散發者」端執行 [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 指定 Oracle 發行者的名稱**@publisher**，值為`xactsetbatching`如**@propertyname**，而值為`enabled`如**@propertyvalue**.  
  
3.  在「散發者」端執行 [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 指定 Oracle 發行者的名稱**@publisher**，值為`xactsetjobinterval`如**@propertyname**，和作業間隔，以分鐘為單位的**@propertyvalue**.  
  
4.  在「散發者」端執行 [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 指定 Oracle 發行者的名稱**@publisher**，值為`xactsetjob`如**@propertyname**，而值為`enabled`如**@propertyvalue**.  
  
### <a name="to-configure-the-transaction-set-job"></a>若要設定交易集作業  
  
1.  (選擇性) 在「散發者」端執行 [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 針對 **@publisher**。 這麼做會傳回「發行者」端 **Xactset** 作業的屬性。  
  
2.  在「散發者」端執行 [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 針對 **@publisher**的「Oracle 發行者」名稱、指定針對 **@propertyname**所設定之 Xactset 作業屬性的名稱，並指定 **@propertyvalue**。  
  
3.  (選擇性) 針對每個要設定的 Xactset 作業屬性重複步驟 2。 變更時`xactsetjobinterval`屬性，您必須重新啟動新的間隔才會生效 「 Oracle 發行者 」 上的作業。  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>若要檢視交易集作業的屬性  
  
1.  在「散發者」端執行 [sp_helpxactsetjob](/sql/relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql)。 針對 **@publisher**。  
  
### <a name="to-disable-the-transaction-set-job"></a>若要停用交易集作業  
  
1.  在「散發者」端執行 [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql)。 指定 Oracle 發行者的名稱**@publisher**，值為`xactsetjob`如**@propertyname**，而值為`disabled`如**@propertyvalue**.  
  
## <a name="example"></a>範例  
 下列範例會啟用 `Xactset` 作業，並在執行之間設定三分鐘的間隔。  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../snippets/tsql/SQL15/replication/howto/tsql/enablexactsetjob.sql#sp_enable_xactsetjob)]  
  
## <a name="see-also"></a>另請參閱  
 [Oracle 發行者的效能微調](../non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  

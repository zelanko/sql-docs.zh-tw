---
title: "針對 SQL Server 資源健全情況 (SQL Server 公用程式) 進行疑難排解 | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 614f07b5-f221-4013-9f8d-22964cf42270
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0a0d583b177984d86f59623f496596db12da0eb2
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="troubleshoot-sql-server-resource-health-sql-server-utility"></a>疑難排解 SQL Server 資源健全情況 (SQL Server 公用程式)
  疑難排解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 找到的資源健全狀況問題可能包括改善電腦或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中 CPU 的過度使用，或是改善資料層應用程式的 CPU 過度使用。 其他問題可能還包括解決資料庫檔案的檔案空間過度使用，或是解決存放磁碟區中配置磁碟空間的過度使用。  
  
 請注意，如果資料庫處於「緊急」狀態，則健全狀態會顯示記錄檔空間過度使用。  
  
 如需 UCP 上受管理的執行個體清單檢視中，因資料收集失敗導致灰色狀態圖示的詳細資訊，請參閱 [疑難排解 SQL Server 公用程式](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式入門的詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
 如需改善 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 所確認之特定資源健全狀況問題的詳細資訊，請參閱下列主題：  
  
-   [如何識別 SQL Server 版本與版本類型](http://go.microsoft.com/fwlink/?LinkID=178504)  
  
-   [疑難排解 SQL Server 2008 的效能問題](http://go.microsoft.com/fwlink/?LinkId=151354)  
  
  

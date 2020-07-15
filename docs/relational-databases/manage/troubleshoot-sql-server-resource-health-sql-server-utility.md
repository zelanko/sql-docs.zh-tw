---
title: 針對 SQL Server 資源健全情況 (SQL Server 公用程式) 進行疑難排解 | Microsoft 文件
description: 了解如何針對 SQL Server UCP 所識別的資源健全狀況問題 (例如使用量過高的 CPU、檔案空間或配置的磁碟空間) 進行疑難排解。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 614f07b5-f221-4013-9f8d-22964cf42270
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cb188aa5a71ef9631aa61ead08cfc33ed1210c7f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85786443"
---
# <a name="troubleshoot-sql-server-resource-health-sql-server-utility"></a>疑難排解 SQL Server 資源健全情況 (SQL Server 公用程式)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  疑難排解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 找到的資源健全狀況問題可能包括改善電腦或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中 CPU 的過度使用，或是改善資料層應用程式的 CPU 過度使用。 其他問題可能還包括解決資料庫檔案的檔案空間過度使用，或是解決存放磁碟區中配置磁碟空間的過度使用。  
  
 請注意，如果資料庫處於「緊急」狀態，則健康狀態會顯示記錄檔空間過度使用。  
  
 如需 UCP 上受管理的執行個體清單檢視中，因資料收集失敗導致灰色狀態圖示的詳細資訊，請參閱 [疑難排解 SQL Server 公用程式](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式入門的詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
 如需改善 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 所確認之特定資源健全狀況問題的詳細資訊，請參閱下列主題：  
  
-   [如何識別 SQL Server 版本與版本類型](https://go.microsoft.com/fwlink/?LinkID=178504)  
  
-   [疑難排解 SQL Server 2008 的效能問題](https://go.microsoft.com/fwlink/?LinkId=151354)  
  
  

---
title: 針對 SQL Server 資源健全情況 (SQL Server 公用程式) 進行疑難排解 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 614f07b5-f221-4013-9f8d-22964cf42270
caps.latest.revision: 6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f34b48f442ffbc64c7c661402890dac8fa0602b9
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814194"
---
# <a name="troubleshoot-sql-server-resource-health-sql-server-utility"></a>疑難排解 SQL Server 資源健全情況 (SQL Server 公用程式)
  疑難排解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 找到的資源健全狀況問題可能包括改善電腦或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中 CPU 的過度使用，或是改善資料層應用程式的 CPU 過度使用。 其他問題可能還包括解決資料庫檔案的檔案空間過度使用，或是解決存放磁碟區中配置磁碟空間的過度使用。  
  
 請注意，如果資料庫處於「緊急」狀態，則健全狀態會顯示記錄檔空間過度使用。  
  
 如需 UCP 上受管理的執行個體清單檢視中，因資料收集失敗導致灰色狀態圖示的詳細資訊，請參閱 [疑難排解 SQL Server 公用程式](../../database-engine/troubleshoot-the-sql-server-utility.md)。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式入門的詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)。  
  
 如需改善 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 所確認之特定資源健全狀況問題的詳細資訊，請參閱下列主題：  
  
-   [如何識別 SQL Server 版本與版本類型](http://go.microsoft.com/fwlink/?LinkID=178504)  
  
-   [疑難排解 SQL Server 2008 的效能問題](http://go.microsoft.com/fwlink/?LinkId=151354)  
  
  

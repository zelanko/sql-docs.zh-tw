---
title: "檢查磁碟輸入輸出子系統的讀取重試問題 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "最佳做法 [Database Engine]"
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# 檢查磁碟輸入輸出子系統的讀取重試問題
  這個規則會檢查事件記錄檔中是否有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤訊息 825。 此訊息表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法在第一次嘗試時讀取磁碟上的資料。 此訊息表示磁碟 I/O 子系統發生重大問題。 此訊息目前並不表示有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 問題。 但是，磁碟問題若沒有解決，可能會導致資料遺失或資料庫損毀。  
  
## 最佳做法建議  
 下列動作可協助您找出並解決根本硬體問題：  
  
-   檢閱錯誤記錄檔和此訊息中的變數文字，找出能夠解釋問題的線索。  
  
-   檢查磁碟系統。 問題可能與磁碟、磁碟控制卡、陣列卡，或磁碟驅動程式有關。  
  
-   連絡磁碟製造廠商，取得最新的公用程式來檢查磁碟系統的狀態。  
  
-   連絡磁碟製造廠商，取得最新的驅動程式更新。  
  
## 詳細資訊  
 [MSSQLSERVER_825](../Topic/MSSQLSERVER_825.md)  
  
 [SQL Server I/O 基本概念，第 2 章](http://go.microsoft.com/fwlink/?linkid=69370)  
  
  
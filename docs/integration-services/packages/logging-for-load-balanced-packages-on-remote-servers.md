---
title: "遠端伺服器上負載平衡封裝的記錄 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "記錄 [Integration Services], 遠端封裝"
ms.assetid: fd571567-b625-4f9a-8b7e-42c5c588b11b
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# 遠端伺服器上負載平衡封裝的記錄
  當所有子封裝都使用相同的記錄提供者，而且全部寫入同一個目的地時，可以讓管理員較容易管理各種伺服器上執行之所有子封裝的記錄檔。 為所有子封裝建立共用記錄檔的其中一個方法，就是透過設定子封裝，使它們將事件記錄到 SQL Server 記錄提供者。 您可以將所有封裝設定成使用同一個資料庫、同一部伺服器，以及伺服器的同一個執行個體。  
  
 若要檢視記錄檔，管理員只需登入單一伺服器即可檢視所有子封裝的記錄檔。  
  
## 相關工作  
 如需如何啟用封裝中記錄的資訊，請參閱[在 SQL Server Data Tools 中啟用封裝記錄功能](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md)。  
  
## 請參閱＜  
 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
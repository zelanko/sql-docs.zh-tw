---
title: "[設定中斷點] | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.setbreakpoints.f1"
helpviewer_keywords: 
  - "設定中斷點對話方塊"
ms.assetid: 876e61b7-875c-43f4-bbce-d7eeb90f6730
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# [設定中斷點]
  使用 **[設定中斷點]** 對話方塊，即可指定要啟用中斷點的事件並控制中斷點的行為。  
  
## 選項。  
 **已啟用**  
 選取即可在事件上啟用中斷點。  
  
 **中斷條件**  
 檢視要設定中斷點之可用事件的清單。  
  
 **叫用計數類型**  
 指定中斷點生效的時間。  
  
|Value|說明|  
|-----------|-----------------|  
|**永遠**|叫用中斷點時，一律暫停執行。|  
|**叫用計數等於**|當中斷點發生的次數等於叫用計數時，暫停執行。|  
|**叫用大於或等於**|當中斷點發生的次數大於或等於叫用計數時，暫停執行。|  
|**叫用計數倍數**|每當到達叫用計數的倍數時，暫停執行。 例如，若您將此選項設定為 5，則每到達五次叫用便會暫停執行。|  
  
 **叫用計數**  
 指定觸發中斷的叫用次數。 如果中斷點永遠有效，則無法使用此選項。  
  
## 請參閱＜  
 [偵錯控制流程](../../integration-services/troubleshooting/debugging-control-flow.md)  
  
  
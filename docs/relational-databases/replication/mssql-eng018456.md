---
title: "MSSQL_ENG018456 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG018456 錯誤"
ms.assetid: 3daa8144-d81f-445a-b6c3-4bb3e9fd1526
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG018456
    
## 訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|18456|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|使用者登入失敗 ' %.* ls'.%。\*ls|  
  
## 說明  
 每當登入嘗試失敗時，都會產生 MSSQL_ENG018456 錯誤。 如果錯誤訊息包含帳戶 **distributor_admin** （登入失敗的使用者 'distributor_admin'。），問題通常是複寫所使用的帳戶。 複寫會建立遠端伺服器， **repl_distributor**, ，可讓 「 散發者 」 與 「 發行者 」 之間的通訊。 登入 **distributor_admin** 此遠端伺服器相關聯，且必須是有效的密碼。  
  
## 使用者動作  
 確定您已為此帳戶指定密碼。 如需詳細資訊，請參閱 [保護散發者](../../relational-databases/replication/security/secure-the-distributor.md)。  
  
## 另請參閱  
 [錯誤和事件參考 & #40。複寫 & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
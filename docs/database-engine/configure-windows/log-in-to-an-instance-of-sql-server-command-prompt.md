---
title: "登入 SQL Server 的執行個體 (命令提示字元) | Microsoft Docs"
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
  - "登入 [SQL Server], SQL Server 具名執行個體"
  - "登入 [SQL Server]"
  - "登入 [SQL Server], SQL Server 預設執行個體"
  - "命令提示字元 [SQL Server], 登入"
  - "登入 [SQL Server]"
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# 登入 SQL Server 的執行個體 (命令提示字元)
  本主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sqlcmd **公用程式測試** 執行個體的連線。  
  
##  <a name="SSMSProcedure"></a>  
  
#### 若要登入 SQL Server 的預設執行個體  
  
1.  在命令提示字元中，輸入下列命令即可使用 [Windows 驗證] 進行連接：  
  
    ```  
    sqlcmd [ /E ] [ /S servername ]  
  
    ```  
  
#### 若要登入 SQL Server 的具名執行個體  
  
1.  在命令提示字元中，輸入下列命令即可使用 [Windows 驗證] 進行連接：  
  
    ```  
    sqlcmd [ /E ] /S servername\instancename  
  
    ```  
  
## 另請參閱  
 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)   
 [osql 公用程式](../../tools/osql-utility.md)  
  
  
---
title: "登入 SQL Server 的執行個體 (命令提示字元) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e672ebb3b8c13a61f0ec2a061195f88ba7c751c4
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>登入 SQL Server 的執行個體 (命令提示字元)
  本主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sqlcmd **公用程式測試** 執行個體的連線。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-log-in-to-the-default-instance-of-sql-server"></a>若要登入 SQL Server 的預設執行個體  
  
1.  在命令提示字元中，輸入下列命令即可使用 [Windows 驗證] 進行連接：  
  
    ```  
    sqlcmd [ /E ] [ /S servername ]  
  
    ```  
  
#### <a name="to-log-in-to-a-named-instance-of-sql-server"></a>若要登入 SQL Server 的具名執行個體  
  
1.  在命令提示字元中，輸入下列命令即可使用 [Windows 驗證] 進行連接：  
  
    ```  
    sqlcmd [ /E ] /S servername\instancename  
  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [sqlcmd 公用程式](../../tools/sqlcmd-utility.md)   
 [osql 公用程式](../../tools/osql-utility.md)  
  
  


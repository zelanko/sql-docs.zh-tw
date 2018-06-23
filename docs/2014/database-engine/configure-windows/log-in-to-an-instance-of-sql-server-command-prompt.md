---
title: 登入 SQL Server 的執行個體 (命令提示字元) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
caps.latest.revision: 23
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 266da633926e1d79236fb0a9f6045b45790c8e49
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145005"
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
  
  
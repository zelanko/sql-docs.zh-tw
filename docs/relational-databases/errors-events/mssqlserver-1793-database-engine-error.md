---
title: MSSQLSERVER_1793 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 808db1d0-acc1-41d0-9287-8a5455001a02
caps.latest.revision: 6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d17e5512007c3aa0a1259114f4f650c23ea6fe0a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver1793"></a>MSSQLSERVER_1793
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|1793|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|FILESTREAM_BASEDATA_NEED_SAME_PARTITION|  
|訊息文字|無法卸除索引 '%.*ls'，因為未指定 FILESTREAM 資料的分割區配置。|  
  
## <a name="explanation"></a>說明  
當您嘗試在包含 FILESTREAM 資料的資料表上卸除叢集索引，而且對基底資料指定 **MOVE TO** 子句，但未對 FILESTREAM 資料指定 **FILESTREAM_ON** 子句時，就會出現這個訊息。  
  
## <a name="user-action"></a>使用者動作  
在包含 FILESTREAM 資料的資料表上卸除叢集索引時，使用下列其中一個選項：  
  
-   對基底資料指定 **MOVE TO** 子句，而且對 FILESTREAM 資料指定 **FILESTREAM_ON** 子句。  
  
-   不對基底資料指定 **MOVE TO** 子句，或對 FILESTREAM 資料指定 **FILESTREAM_ON** 子句。  
  
下列範例失敗，因為指定基底資料的分割區配置，但未指定 FILESTREAM 資料的分割區配置。  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY] )  
GO  
```  
  
下列範例成功，因為對基底資料指定 **MOVE TO** 子句，而且對 FILESTREAM 資料指定 **FILESTREAM_ON** 子句。  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF, MOVE TO [PRIMARY], filestream_on 'default' )  
GO  
```  
  
下列範例也成功，因為未對基底資料指定 **MOVE TO** 子句，也未對 FILESTREAM 資料指定 **FILESTREAM_ON** 子句。  
  
```Transact-SQL  
DROP INDEX [<clustered_index_name>] ON [<table_name>]   
WITH ( ONLINE = OFF )  
GO  
```  
  

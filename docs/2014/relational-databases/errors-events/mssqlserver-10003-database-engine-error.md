---
title: MSSQLSERVER_10003 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10003 (Database Engine error)
ms.assetid: 9e2cb199-f077-4d88-8117-1b7550afc696
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f7e5a3b7c5b639b5ded1ea7dfd357a93375781b1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203588"
---
# <a name="mssqlserver10003"></a>MSSQLSERVER_10003
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|10003|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|HR_E_OUTOFMEMORY|  
|訊息文字|提供者已用完記憶體。|  
  
## <a name="explanation"></a>說明  
 系統記憶體不足導致 OLE DB 提供者用完記憶體。  
  
## <a name="user-action"></a>使用者動作  
 重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 如果這樣做沒有用，請重新啟動電腦。 如果持續發生此問題，請使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 來收集 OLE DB 追蹤事件，並提供這項資料給 OLE DB 提供者的產品支援部門。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Profiler 範本和權限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  

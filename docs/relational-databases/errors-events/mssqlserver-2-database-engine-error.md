---
title: MSSQLSERVER_2 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- "2"
helpviewer_keywords:
- 2 (Database Engine error)
ms.assetid: 567fb571-7cda-4ce8-a702-cdff2df5d419
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d970b6571456ce5a531a393b3a483d48b24d90d4
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34321749"
---
# <a name="mssqlserver2"></a>MSSQLSERVER_2
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|2|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|建立伺服器的連接時發生錯誤。  連接到 SQL Server 時，可能因為在預設的設定下 SQL Server 不允許遠端連接而引起此失敗。 (提供者: 具名管道提供者，錯誤: 40 - 無法開啟至 SQL Server 的連接) (.Net SqlClient 資料提供者)|  
  
## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法回應用戶端要求，可能是因為伺服器尚未啟動。  
  
## <a name="user-action"></a>使用者動作  
請確定伺服器已經啟動。  
  
## <a name="see-also"></a>另請參閱  
[管理 Database Engine Services](~/database-engine/configure-windows/manage-the-database-engine-services.md)  
[設定用戶端通訊協定](~/database-engine/configure-windows/configure-client-protocols.md)  
[網路通訊協定和網路程式庫](~/sql-server/install/network-protocols-and-network-libraries.md)  
[用戶端網路組態](~/database-engine/configure-windows/client-network-configuration.md)  
[設定用戶端通訊協定](~/database-engine/configure-windows/configure-client-protocols.md)  
[啟用或停用伺服器網路通訊協定](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  

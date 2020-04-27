---
title: MSSQLSERVER_10061 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- "10061"
helpviewer_keywords:
- 10061 (Database Engine error)
ms.assetid: 729602f3-08df-474c-8740-8dea13c1eee3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b77e1d920f97891d173bfdcdcb23ceb6c0acf0c4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62870706"
---
# <a name="mssqlserver_10061"></a>MSSQLSERVER_10061
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|10061|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|建立伺服器的連接時發生錯誤。  連接到 SQL Server 時，可能因為在預設的設定下 SQL Server 不允許遠端連接而引起此失敗。 (提供者: TCP 提供者，錯誤: 0 - 無法連線，因為目標電腦拒絕連線。) (Microsoft SQL Server，錯誤: 10061)|  
  
## <a name="explanation"></a>說明  
 伺服器並未回應用戶端要求。 發生這個錯誤可能是因為伺服器尚未啟動。  
  
## <a name="user-action"></a>使用者動作  
 請確定伺服器已經啟動。  
  
## <a name="see-also"></a>另請參閱  
 [管理資料庫引擎服務](../../database-engine/configure-windows/manage-the-database-engine-services.md)   
 [設定用戶端通訊協定](../../database-engine/configure-windows/configure-client-protocols.md)   
 [網路通訊協定和網路程式庫](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [用戶端網路設定](../../database-engine/configure-windows/client-network-configuration.md)   
 [設定用戶端通訊協定](../../database-engine/configure-windows/configure-client-protocols.md)   
 [啟用或停用伺服器網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  

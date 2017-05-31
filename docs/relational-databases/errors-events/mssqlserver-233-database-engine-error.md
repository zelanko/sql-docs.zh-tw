---
title: MSSQLSERVER_233 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "233"
helpviewer_keywords:
- 233 (Database Engine error)
ms.assetid: 201665dc-7ac8-4c19-90d3-33354c5caa72
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a029352dec1ac5a700b7ad5d048a9cb630347462
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver233"></a>MSSQLSERVER_233
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|233|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|已順利建立與伺服器的連接，但隨後在登入過程中發生錯誤。 (提供者: 共用記憶體提供者，錯誤: 0 - 在管道的另一端沒有處理序。) (Microsoft SQL Server，錯誤: 233)|  
  
## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端無法連接到伺服器。 發生這個錯誤可能是因為伺服器未設定成接受遠端連接。  
  
## <a name="user-action"></a>使用者動作  
使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員工具，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定成接受遠端連接。  
  
## <a name="see-also"></a>另請參閱  
[網路通訊協定和網路程式庫](~/sql-server/install/network-protocols-and-network-libraries.md)  
[用戶端網路組態](~/database-engine/configure-windows/client-network-configuration.md)  
[設定用戶端通訊協定](~/database-engine/configure-windows/configure-client-protocols.md)  
[啟用或停用伺服器網路通訊協定](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  


---
title: MSSQLSERVER_233 | Microsoft Docs
description: SQL Server 用戶端無法連線到伺服器。 請參閱錯誤的說明及可能的解決方法。
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "233"
helpviewer_keywords:
- 233 (Database Engine error)
ms.assetid: 201665dc-7ac8-4c19-90d3-33354c5caa72
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 87c312289b9a2a8ed7e0ae9d97a4993121772721
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780467"
---
# <a name="mssqlserver_233"></a>MSSQLSERVER_233
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|233|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|已順利建立與伺服器的連接，但隨後在登入過程中發生錯誤。 (提供者：共用記憶體提供者，錯誤:0 - 管道的另一端上無任何處理程序。) (Microsoft SQL Server，錯誤:233)|  
  
## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端無法連接到伺服器。 發生這個錯誤可能是因為伺服器未設定成接受遠端連接。  
  
## <a name="user-action"></a>使用者動作  
使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員工具，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定成接受遠端連接。  
  
## <a name="see-also"></a>另請參閱  
[網路通訊協定和網路程式庫](~/sql-server/install/network-protocols-and-network-libraries.md)  
[用戶端網路組態](~/database-engine/configure-windows/client-network-configuration.md)  
[設定用戶端通訊協定](~/database-engine/configure-windows/configure-client-protocols.md)  
[啟用或停用伺服器網路通訊協定](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  

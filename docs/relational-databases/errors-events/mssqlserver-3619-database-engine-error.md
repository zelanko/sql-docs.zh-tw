---
description: MSSQLSERVER_3619
title: MSSQLSERVER_3619 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3619 (Database Engine error)
ms.assetid: 7d94f8d9-65ca-4fde-9c17-7b83e94a3779
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dce607f8284eff4c8808ce08d41879e38788e7f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456170"
---
# <a name="mssqlserver_3619"></a>MSSQLSERVER_3619
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|3619|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SYS_NOLOG|  
|訊息文字|無法在資料庫識別碼 %d 中寫入檢查點記錄，因為記錄空間不足。 請連絡資料庫管理員截斷記錄，或者配置更多的空間給資料庫記錄檔。|  
  
## <a name="explanation"></a>說明  
交易記錄磁碟空間不足。  
  
## <a name="user-action"></a>使用者動作  
截斷記錄以釋出部分空間，或配置更多空間給記錄檔。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜寫滿交易記錄疑難排解 (錯誤 9002)＞。  
  

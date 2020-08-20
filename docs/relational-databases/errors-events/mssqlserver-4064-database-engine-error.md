---
description: MSSQLSERVER_4064
title: MSSQLSERVER_4064 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4064 (Database Engine error)
ms.assetid: 32112b90-0a2f-4834-a027-756811732be7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 27f5ccbad0bd1722f8c9a4fbe1d2b7cd0fd633da
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471077"
---
# <a name="mssqlserver_4064"></a>MSSQLSERVER_4064
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|4064|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DB_UFAIL_FATAL|  
|訊息文字|無法開啟使用者預設資料庫。 登入失敗。|  
  
## <a name="explanation"></a>說明  
由於預設資料庫發生問題，SQL Server 登入無法連接。 可能是資料庫本身無效，或是登入在資料庫上沒有 CONNECT 權限。  
  
## <a name="user-action"></a>使用者動作  
使用 ALTER LOGIN 變更登入的預設資料庫。 授與 CONNECT 權限給登入。  
  

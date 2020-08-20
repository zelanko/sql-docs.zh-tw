---
description: MSSQLSERVER_3452
title: MSSQLSERVER_3452 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5eaf8a280ebc3da3c1313010d336f5fa0ef67c1a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456185"
---
# <a name="mssqlserver_3452"></a>MSSQLSERVER_3452
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|3452|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|REC_CHECKIDENTITY|  
|訊息文字|資料庫 '%.*ls' (%d) 的復原偵測到資料表識別碼 %d 中的識別值可能不一致。 請執行 DBCC CHECKIDENT ('%.\*ls')。|  
  
## <a name="explanation"></a>說明  
升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 時，復原資料庫中識別值的處理序在中繼資料中發現不一致的問題。  
  
## <a name="user-action"></a>使用者動作  
執行 DBCC CHECKIDENT。  
  

---
description: MSSQLSERVER_1807
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5b6b4d42d13539d62f7afc7cc341f2b7b1bee44f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456305"
---
# <a name="mssqlserver_1807"></a>MSSQLSERVER_1807
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|1807|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|CANNOT_EX_LOCK|  
|訊息文字|無法取得資料庫 '%.*ls' 的獨佔鎖定。 請稍後再重試作業。|  
  
## <a name="explanation"></a>說明  
需要獨佔存取資料庫的作業無法取得適當的存取權。  
  
## <a name="user-action"></a>使用者動作  
中斷該資料庫的所有連接，或稍後再重試查詢。  
  

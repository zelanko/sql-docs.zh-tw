---
description: MSSQLSERVER_611
title: MSSQLSERVER_611 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 611 (Database Engine error)
ms.assetid: ac6a213f-5c38-44ad-bc85-a62863786614
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 33076c77372ac62f154fbe5d3c60273447be99e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470958"
---
# <a name="mssqlserver_611"></a>MSSQLSERVER_611
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|611|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|VAR_SIZE_TOO_BIG|  
|訊息文字|無法插入或更新資料列，因為變數資料行的總大小 (包括負擔) 要比限制多出 %d 個位元組。|  
  
## <a name="explanation"></a>說明  
變數資料行大小上限多於結構描述允許的值。 當變數資料行大小超出啟用 Vardecimal 資料格式時固定案例中的限制，或是變數資料行大小超出 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 壓縮資料記錄所允許的限制時，就會傳回錯誤 611。  
  
## <a name="user-action"></a>使用者動作  
縮減此記錄的大小。  
  

---
title: MSSQLSERVER_1807 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 1807 (Database Engine error)
ms.assetid: 13c1b240-098b-4d9e-89aa-21599548e074
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e7102630e638d891345c47ed8d9f92700fde39aa
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver1807"></a>MSSQLSERVER_1807
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
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
  


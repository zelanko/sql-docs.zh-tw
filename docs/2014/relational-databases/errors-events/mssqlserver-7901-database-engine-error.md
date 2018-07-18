---
title: MSSQLSERVER_7901 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 7901 (Database Engine error)
ms.assetid: 2d0d19b9-947b-4474-9ff8-7e03019ab93d
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ea29b3ef2bc08e3451f402f17bed298b982f1bc2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407547"
---
# <a name="mssqlserver7901"></a>MSSQLSERVER_7901
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|7901|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC2_DATABASE_IN_EMERGENCY_MODE|  
|訊息文字|未處理修復陳述式。 當資料庫處於緊急模式時不支援此修復層級。|  
  
## <a name="explanation"></a>說明  
 資料庫正處於緊急模式，而且已經指定了 REPAIR_ALLOW_DATA_LOSS 以外的修復層級。 除非指定 REPAIR_ALLOW_DATA_LOSS，否則不能在緊急模式下進行修復。  
  
## <a name="user-action"></a>使用者動作  
 重新執行命令，並指定 REPAIR_ALLOW_DATA_LOSS 選項。  
  
  

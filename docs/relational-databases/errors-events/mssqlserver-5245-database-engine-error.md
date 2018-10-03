---
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a5a1c3882a310a5fb0debb52ccfc7c0e7cdd35de
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825539"
---
# <a name="mssqlserver5245"></a>MSSQLSERVER_5245
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|5245|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|訊息文字|物件識別碼 O_ID (物件 'NAME'): DBCC 無法在此物件上取得鎖定，因為已超過鎖定要求逾時期間。 已經略過這個物件，不會處理。|  
  
## <a name="explanation"></a>說明  
DBCC 等候指定物件的資料表鎖定時發生鎖定逾時。  
  
## <a name="user-action"></a>使用者動作  
重新執行 DBCC 命令。  
  

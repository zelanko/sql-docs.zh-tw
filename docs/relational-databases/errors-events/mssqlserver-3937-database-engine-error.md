---
title: MSSQLSERVER_3937 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3937 (Database Engine error)
ms.assetid: 312d5bbe-c8de-42db-af4b-4ccb448ce6ef
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3cb93f99d996cc992fc47873b2a3863caec7ec6d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63028752"
---
# <a name="mssqlserver3937"></a>MSSQLSERVER_3937
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|MSSQLSERVER|  
|事件識別碼|3937|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|XACT_FILESTREAM_ROLLBACK_ERROR|  
|訊息文字|嘗試通知檔案資料流篩選驅動程式已回復交易時發生錯誤。 錯誤碼：0x%0x。|  
  
## <a name="explanation"></a>說明  
當發出交易的回復通知時，RsFx 驅動程式傳回了錯誤。 這可能是因為資源短缺所造成。 這會造成 RsFx 篩選驅動程式內的小型記憶體遺漏，但是當建立交易的 sqlservr.exe 處理序結束時，將會釋出這些記憶體。  
  
## <a name="user-action"></a>使用者動作  

---
title: MSSQLSERVER_17803 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17803 (Database Engine error)
ms.assetid: 28591a19-258d-4891-b78a-4686789bb2d7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ac4c4c08c13a700e795ddad0901c0c43829d623f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780745"
---
# <a name="mssqlserver_17803"></a>MSSQLSERVER_17803
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|17803|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SRV_NOMEMORY|  
|訊息文字|建立連接期間發生記憶體配置錯誤。 請減少非必要的記憶體載入，或增加系統記憶體。 此連接已經關閉。%.*ls|  
  
## <a name="explanation"></a>說明  
伺服器記憶體不足。  
  
## <a name="user-action"></a>使用者動作  
判斷伺服器記憶體不足的原因。 一般記憶體疑難排解步驟可能會很有用。  
  

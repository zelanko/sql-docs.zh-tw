---
title: MSSQLSERVER_17132 | Microsoft Docs
description: SQL Server 電腦無法處理用戶端登入封包。 請參閱錯誤的說明及可能的解決方法。
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17132 (Database Engine error)
ms.assetid: d1d198bd-6730-4394-bd5f-28f320c01a38
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4767ba217eab0d8cdbc6a9dc80f751868322f21f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780845"
---
# <a name="mssqlserver_17132"></a>MSSQLSERVER_17132
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|17132|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|INIT_NODESSPACE|  
|訊息文字|由於描述項的記憶體不足使伺服器無法啟動。 請減少非必要的記憶體載入或增加系統記憶體。|  
  
## <a name="explanation"></a>說明  
無法配置足夠的記憶體來儲存伺服器內部描述項。  
  
## <a name="user-action"></a>使用者動作  
為電腦增加更多記憶體。 一般記憶體疑難排解步驟可能會很有用。  
  

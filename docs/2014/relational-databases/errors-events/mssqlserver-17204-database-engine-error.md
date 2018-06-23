---
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e3326f262e63c658589032688c82827e86d93a9b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145153"
---
# <a name="mssqlserver17204"></a>MSSQLSERVER_17204
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|17204|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBLKIO_DEVOPENFAILED|  
|訊息文字|%ls: 無法開啟檔案 %ls，檔案編號為 %d。  作業系統錯誤: %ls。|  
  
## <a name="explanation"></a>說明  
 SQL Server 無法開啟指定的檔案，因為發生指定的錯誤。  
  
## <a name="user-action"></a>使用者動作  
 診斷並更正作業系統，然後重試此作業。  
  
  
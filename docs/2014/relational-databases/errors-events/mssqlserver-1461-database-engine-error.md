---
title: MSSQLSERVER_1461 | Microsoft Docs
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
- 1461 (Database Engine error)
ms.assetid: fce10907-4753-441b-b624-f28e00ed7520
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 663aeec8ff61ce1717392c32d4f97e71403d1b5c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033647"
---
# <a name="mssqlserver1461"></a>MSSQLSERVER_1461
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|1461|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|DBM_SAFETY_MISMATCH|  
|訊息文字|在各伺服器上偵測到資料庫 "%.*ls" 的不同資料庫鏡像安全性層級。 將會使用 FULL 安全性層級。|  
  
## <a name="explanation"></a>說明  
 由於主體和鏡像資料庫上的交易安全性設定不一致，因此，當修改交易安全性層級時，鏡像連接會中斷。 將會使用完整交易安全性的預設安全性設定。 工作階段將以高安全性模式執行。  
  
## <a name="user-action"></a>使用者動作  
 若要將交易安全性設為關閉，請在主體資料庫上重新執行 ALTER DATABASE *database_name* SET PARTNER SAFETY OFF 陳述式。  
  
  
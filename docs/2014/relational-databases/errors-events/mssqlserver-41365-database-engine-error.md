---
title: MSSQLSERVER_41365 | Microsoft Docs
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
- 41365 (Database Engine error)
ms.assetid: 4fc7ec15-b722-4e3d-b7f9-3d39d171e96e
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d448d82a6a0067a1bb3eca56a83ad47852e680d2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036345"
---
# <a name="mssqlserver41365"></a>MSSQLSERVER_41365
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|41365|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|HK_MERGE_SCHEDULE_ERROR|  
|訊息文字|未排程資料庫 %.*ls 上交易範圍 [%ld, %ld] 的合併要求。 代表範圍的檢查點檔案無法用於合併或是正在進行合併的一部分。|  
  
## <a name="explanation"></a>說明  
 代表範圍的檢查點檔案無法用於合併或是正在進行合併的一部分。  
  
## <a name="user-action"></a>使用者動作  
 為合併/等候提供較佳的交易範圍，然後重新發出相同的要求。 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
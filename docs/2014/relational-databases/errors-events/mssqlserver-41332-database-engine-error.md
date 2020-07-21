---
title: MSSQLSERVER_41332 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a35ebcf72195975a69db5b1f1c4e40d987a750a5
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551421"
---
# <a name="mssqlserver_41332"></a>MSSQLSERVER_41332
    
## <a name="details"></a>詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|41332|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQL_SNAPSHOT_NOT_SUPPORTED|  
|訊息文字|工作階段 TRANSACTION ISOLATION LEVEL 設為 SNAPSHOT 時，無法存取或建立記憶體最佳化資料表和原生編譯預存程序。|  
  
## <a name="explanation"></a>說明  
 交易會以快照集隔離等級啟動，然後嘗試使用不相容的功能。  
  
## <a name="user-action"></a>使用者動作  
 以不同的隔離等級啟動交易。 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

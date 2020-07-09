---
title: MSSQLSERVER_41365 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41365 (Database Engine error)
ms.assetid: 4fc7ec15-b722-4e3d-b7f9-3d39d171e96e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 841ea749faa87d66216754ce3aabb61c03d6f996
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765308"
---
# <a name="mssqlserver_41365"></a>MSSQLSERVER_41365
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|41365|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|HK_MERGE_SCHEDULE_ERROR|  
|訊息文字|未排程資料庫 %.*ls 上交易範圍 [%ld, %ld] 的合併要求。 代表範圍的檢查點檔案無法用於合併或是正在進行合併的一部分。|  
  
## <a name="explanation"></a>說明  
代表範圍的檢查點檔案無法用於合併或是正在進行合併的一部分。  
  
## <a name="user-action"></a>使用者動作  
為合併/等候提供較佳的交易範圍，然後重新發出相同的要求。 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱  
[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

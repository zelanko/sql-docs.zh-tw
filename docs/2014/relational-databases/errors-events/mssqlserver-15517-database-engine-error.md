---
title: MSSQLSERVER_15517 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 15517 (Database Engine error)
ms.assetid: f94287f5-129f-4c52-9d34-62b996088001
caps.latest.revision: 5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ebbc87a299cb55658c7a8506fa4a63a2e2d1d215
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426467"
---
# <a name="mssqlserver15517"></a>MSSQLSERVER_15517
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|15517|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SEC_CANNOTEXECUTEASUSER|  
|訊息文字|無法以資料庫主體執行，因為主體 "*principal*" 不存在、無法模擬這種主體，或者您沒有權限。|  
  
## <a name="user-action"></a>使用者動作  
 使用現有主體的名稱，或取得該主體的 IMPERSONATE 權限。  
  
 15517 也可能在原始資料庫擁有者以外的人執行附加和還原資料庫之後發生。 若要解決此錯誤，請執行下列命令將 db_owner 變更為伺服器上的登入：  
  
```  
ALTER AUTHORIZATION ON DATABASE:: DBName TO [NewLogin]  
```  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

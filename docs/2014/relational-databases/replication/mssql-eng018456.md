---
title: MSSQL_ENG018456 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG018456 error
ms.assetid: 3daa8144-d81f-445a-b6c3-4bb3e9fd1526
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 343abeb430a09eb1dcd6375266bb314e5f61c509
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132853"
---
# <a name="mssqleng018456"></a>MSSQL_ENG018456
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|18456|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|使用者 '%.*ls'.%.\*ls 登入失敗|  
  
## <a name="explanation"></a>說明  
 每當登入嘗試失敗時，都會產生 MSSQL_ENG018456 錯誤。 如果錯誤訊息包含帳戶 **distributor_admin** (使用者 'distributor_admin' 登入失敗)，則為複寫所用帳戶的問題。 複寫建立遠端伺服器， **repl_distributor**，可允許在散發者和發行者之間通訊。 登入 **distributor_admin** 與此遠端伺服器相關聯，且必須具備有效的密碼。  
  
## <a name="user-action"></a>使用者動作  
 確定您已為此帳戶指定密碼。 如需詳細資訊，請參閱[保護散發者](security/secure-the-distributor.md)。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤和事件參考 &#40;複寫&#41;](errors-and-events-reference-replication.md)  
  
  
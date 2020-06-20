---
title: MSSQL_ENG018456 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG018456 error
ms.assetid: 3daa8144-d81f-445a-b6c3-4bb3e9fd1526
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2f83f3b3eeb4375fc71db8ac8988980ab86208d1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85005566"
---
# <a name="mssql_eng018456"></a>MSSQL_ENG018456
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
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
  
  

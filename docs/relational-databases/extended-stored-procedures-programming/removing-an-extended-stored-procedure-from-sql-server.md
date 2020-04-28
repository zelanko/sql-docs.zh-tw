---
title: 移除擴充預存程式
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: ec61cf630d606977689d3fb3763cce8bd8b705c8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74095440"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>從 SQL Server 中移除擴充預存程序
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 若要將每個擴充預存程式函數放在使用者定義的擴充預存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]程式 DLL 中，系統管理員必須執行**sp_dropextendedproc**系統預存程式，並指定函式的名稱以及該函式所在的 DLL 名稱。 例如，此命令會從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]下列位置移除名為 XP_HELLO 的 dll 中的函式**xp_hello**：  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 從開始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]， **sp_dropextendedproc**不會卸載系統擴充預存程式。 相反地，系統管理員應該拒絕將擴充預存程式的 EXECUTE 許可權授與**public**角色。  
  
## <a name="see-also"></a>另請參閱  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  

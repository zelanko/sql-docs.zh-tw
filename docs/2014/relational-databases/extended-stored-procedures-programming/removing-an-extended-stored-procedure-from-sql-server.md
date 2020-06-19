---
title: 從 SQL Server 中移除擴充預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 284da815de073248669da032c06ddeeb68c697a3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85027015"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>從 SQL Server 中移除擴充預存程序
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 若要將每個擴充預存程式函數放在使用者定義的擴充預存程式 DLL 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員必須執行**sp_dropextendedproc**系統預存程式，並指定函式的名稱以及該函式所在的 DLL 名稱。 例如，此命令會從下列位置移除名為 xp_hello.dll 的 DLL 中的函式**xp_hello** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ：  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 從開始 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ， **sp_dropextendedproc**不會卸載系統擴充預存程式。 相反地，系統管理員應該拒絕將擴充預存程式的 EXECUTE 許可權授與**public**角色。  
  
## <a name="see-also"></a>另請參閱  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  

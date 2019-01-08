---
title: 移除擴充預存程序，從 SQL Server |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: bcb58ac180861641803147d1dfea621bd52df9a6
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804020"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>從 SQL Server 中移除擴充預存程序
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 若要卸除使用者定義擴充預存程序 DLL 中的每個擴充預存程序函式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系統管理員必須執行**sp_dropextendedproc**系統預存程序中，指定的名稱函式，該函式所在 DLL 名稱。 例如，此命令會移除函式**xp_hello**，位於從名為 xp_hello.dll 的 DLL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 開頭[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]， **sp_dropextendedproc**未卸除系統擴充預存程序。 相反地，由系統管理員應該拒絕擴充預存程序的 EXECUTE 權限**公開**角色。  
  
## <a name="see-also"></a>另請參閱  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  

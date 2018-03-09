---
title: "擴充預存程序運作方式 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eb9c6663cd2891669140c7eb59e44e110f3d5607
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="how-extended-stored-procedures-work"></a>擴充預存程序運作方式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 擴充預存程序藉以運作的程序為：  
  
1.  當用戶端執行擴充預存程序時，在表格式資料流 (TDS) 或簡易物件存取通訊協定 (SOAP) 格式，從用戶端應用程式傳輸要求[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 搜尋與擴充預存程序相關聯的 DLL，並將 DLL 載入，如果尚未載入。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 呼叫要求的擴充預存程序 （實作為 DLL 內部的函式）。  
  
4.  擴充預存程序會傳遞結果集，並透過擴充預存程序 API 將參數傳回至伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 擴充預存程序程式設計](../../relational-databases/database-engine-extended-stored-procedure-programming.md)  
  
  

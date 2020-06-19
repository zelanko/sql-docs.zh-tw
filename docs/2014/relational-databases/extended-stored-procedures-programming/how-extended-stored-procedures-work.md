---
title: 擴充預存程式的工作方式 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
author: rothja
ms.author: jroth
ms.openlocfilehash: 75082fed6b70c214b4f55b85034ffa371824d24f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85027126"
---
# <a name="how-extended-stored-procedures-work"></a>擴充預存程序運作方式
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 擴充預存程序藉以運作的程序為：  
  
1.  當用戶端執行擴充預存程式時，會從用戶端應用程式以表格式資料流程（TDS）或簡單物件存取通訊協定（SOAP）格式將要求傳送至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會搜尋與擴充預存程序相關聯的 DLL，並載入 DLL (如果尚未載入)。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會呼叫要求的擴充預存程序 (以 DLL 內部的函數實作)。  
  
4.  擴充預存程序會傳遞結果集，並透過擴充預存程序 API 將參數傳回至伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [資料庫引擎擴充預存程序程式設計](../database-engine-extended-stored-procedure-programming.md)  
  
  

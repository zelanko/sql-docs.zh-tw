---
title: 擴充預存程式的工作方式 |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], about extended stored procedures
ms.assetid: 6e946d8c-3268-4b59-8a1c-1637909cd701
author: rothja
ms.author: jroth
ms.openlocfilehash: 02a1c64974fdcab5a686a61ac35a3a2175e16314
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758084"
---
# <a name="how-extended-stored-procedures-work"></a>擴充預存程序運作方式

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 擴充預存程序藉以運作的程序為：  
  
1.  當用戶端執行擴充預存程式時，會從用戶端應用程式以表格式資料流程（TDS）或簡單物件存取通訊協定（SOAP）格式將要求傳送至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會搜尋與擴充預存程序相關聯的 DLL，並載入 DLL (如果尚未載入)。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會呼叫要求的擴充預存程序 (以 DLL 內部的函數實作)。  
  
4.  擴充預存程序會傳遞結果集，並透過擴充預存程序 API 將參數傳回至伺服器。  


---
description: 擴充預存程序運作方式
title: 擴充預存程式的運作方式 |Microsoft Docs
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
ms.openlocfilehash: 49c5f3491d93ee71a0ce118a5f4ba387da770f1c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460813"
---
# <a name="how-extended-stored-procedures-work"></a>擴充預存程序運作方式

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 請改用 CLR 整合。  
  
 擴充預存程序藉以運作的程序為：  
  
1.  當用戶端執行擴充預存程式時， (TDS) 或簡單物件存取通訊協定 (SOAP) 格式從用戶端應用程式傳輸到的要求會傳輸到表格式資料流程中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會搜尋與擴充預存程序相關聯的 DLL，並載入 DLL (如果尚未載入)。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會呼叫要求的擴充預存程序 (以 DLL 內部的函數實作)。  
  
4.  擴充預存程序會傳遞結果集，並透過擴充預存程序 API 將參數傳回至伺服器。  


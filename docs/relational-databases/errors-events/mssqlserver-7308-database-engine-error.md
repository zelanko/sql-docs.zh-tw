---
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 64e662ebf9354f3d1ff48bb5870bd19d367dea9c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780215"
---
# <a name="mssqlserver_7308"></a>MSSQLSERVER_7308
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|7308|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|RMT_STA_DISABLED|  
|訊息文字|OLE DB 提供者 '%ls' 不能用來散佈查詢，因為提供者是設定成以單一執行緒 Apartment 模式執行。|  
  
## <a name="explanation"></a>說明  
您已經使用設定成以單一執行緒 Apartment (STA) 模式執行的 OLE DB 提供者。 以單一執行緒 Apartment (STA) 模式執行的 OLE DB 提供者無法用於分散式查詢。  
  
## <a name="user-action"></a>使用者動作  
若要解決這個錯誤，請將提供者設定成以多執行緒 Apartment (MTA) 模式執行。 如果此提供者不支援 MTA，而且此提供者無法升級為支援 MTA 的版本，請考慮將此提供者設定為跨處理序執行。 提供者供應商應該能夠告訴您此提供者是否支援 MTA 或跨處理序執行。  
  

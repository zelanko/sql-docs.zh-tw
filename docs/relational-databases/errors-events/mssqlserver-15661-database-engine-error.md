---
title: MSSQLSERVER_15661 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15661 (Database Engine error)
ms.assetid: 88b01bfb-74ce-4aa0-aec0-7885261c7ef3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9de47387d8e40d19967f71071f31e14592a376ca
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780940"
---
# <a name="mssqlserver_15661"></a>MSSQLSERVER_15661
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|15661|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SQLErrorNum15661|  
|訊息文字|sp_estimate_data_compression_savings 預存程序無法用於暫存資料表。|  
  
## <a name="explanation"></a>說明  
暫存資料表當做 sp_estimate_data_compression_savings 預存程序的引數使用。 雖然暫存資料表的壓縮有受到支援，但是您無法使用 sp_estimate_data_compression_savings 來預估所節省的壓縮。  
  
## <a name="user-action"></a>使用者動作  
移除當做 sp_estimate_data_compression_savings 之引數的暫存資料表。  
  

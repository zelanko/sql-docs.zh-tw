---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1b5348d31c1b85d3f83797bef186362d62e36efb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85636181"
---
# <a name="mssqlserver_9692"></a>MSSQLSERVER_9692
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|9692|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SB2_CANT_LISTEN_PORT_IN_USE|  
|訊息文字|%S_MSG 通訊協定傳輸無法在連接埠 %d 上接聽，因為它正由另一個處理序所使用。|  
  
## <a name="explanation"></a>說明  
電腦上的另一個程式正在使用指定的 TCP 通訊埠。  
  
## <a name="user-action"></a>使用者動作  
執行 **netstat -aon**，確定哪一個程式正在使用連接埠。 停用該應用程式，或者為 Service Broker 指定不同的通訊埠。  
  

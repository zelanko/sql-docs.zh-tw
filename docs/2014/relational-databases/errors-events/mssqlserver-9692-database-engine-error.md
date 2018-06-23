---
title: MSSQLSERVER_9692 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 9692 (Database Engine error)
ms.assetid: 02399d6e-ab5e-4f30-8a3e-2bb1e8c135b5
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 396f1ae8e711157bc8f6b911997557f68e397c47
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36037019"
---
# <a name="mssqlserver9692"></a>MSSQLSERVER_9692
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|9692|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|SB2_CANT_LISTEN_PORT_IN_USE|  
|訊息文字|%S_MSG 通訊協定傳輸無法在通訊埠 %d 上接聽，因為它正由另一個處理序所使用。|  
  
## <a name="explanation"></a>說明  
 電腦上的另一個程式正在使用指定的 TCP 通訊埠。  
  
## <a name="user-action"></a>使用者動作  
 執行`netstat -aon`來判斷哪一個程式正在使用連接埠。 停用該應用程式，或者為 Service Broker 指定不同的通訊埠。  
  
  
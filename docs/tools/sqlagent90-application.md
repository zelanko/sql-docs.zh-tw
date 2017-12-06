---
title: "sqlagent90 應用程式 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sqlagent
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- starting SQL Server Agent
- sqlagent90 application
- SQL Server Agent, starting
- command prompt utilities [SQL Server], sqlagent90
ms.assetid: e8b80e8d-d0c9-4500-a868-0ce08233da08
caps.latest.revision: "34"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bc67b1f9e76169e48262371fd7472a0c2235f4d4
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="sqlagent90-application"></a>sqlagent90 應用程式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]**Sqlagent90**應用程式啟動[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]代理程式從命令提示字元。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 通常應該從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 執行，或利用應用程式中的 SQL-SMO 方法來執行。 請只在診斷 **Agent 時，或您的主要支援提供者指示您這麼做時，才從命令提示字元執行** sqlagent90 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。  
  
## <a name="syntax"></a>語法  
  
```  
  
sqlagent90  
-c [-v] [-i instance_name]  
```  
  
## <a name="arguments"></a>引數  
 **-c**  
 指出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 是在命令提示字元之下執行，與 Microsoft Windows 服務控制管理員無關。 當使用 **-c** 時， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 無法利用 [系統管理工具] 中的 [服務] 應用程式來控制，也無法利用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員來控制。 這是強制引數。  
  
 **-v**  
 指出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 執行詳細模式，且將診斷資訊寫入命令提示字元視窗中。 診斷資訊與寫入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 錯誤記錄的資訊相同。  
  
 **-i** <執行個體名稱>  
 指出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 連接到 <執行個體名稱> 所指定的具名 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體。  
  
## <a name="remarks"></a>備註  
 顯示著作權訊息之後，只有在指定了 **-v** 參數的情況下， **sqlagent90** 才會在命令提示字元視窗中顯示輸出。 若要停止 **sqlagent90**，請在命令提示字元按 CTRL+C。 在停止 **sqlagent90**之前，請勿關閉命令提示字元視窗。  
  
## <a name="see-also"></a>另請參閱  
 [自動化管理工作 &#40;SQL Server Agent&#41;](http://msdn.microsoft.com/library/541ee5ac-2c9f-4b74-b4f0-13b7bd5920b0)  
  
  

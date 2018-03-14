---
title: "產生 SQL 指令碼 (複寫物件) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.generatesqlscript.f1
helpviewer_keywords:
- Generate SQL Script dialog box
ms.assetid: b7ccc34e-1c22-44b8-8eb5-f6423af3164e
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ffc0fd061540ec62aae33b2269035d4d63067725
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/08/2018
---
# <a name="generate-sql-script-replication-objects"></a>產生 SQL 指令碼 (複寫物件)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  複寫指令碼包含要實作已編寫複寫元件之指令碼所必要的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 系統預存程序，例如發行集或訂閱。 拓撲中的所有複寫元件都應作為損毀復原計畫的一部份來編寫指令碼，而指令碼也可以用於自動執行重複性工作。 複寫提供編寫複寫物件之指令碼的兩個對話方塊：  
  
-   **[產生 SQL 指令碼]**，這可從 **msCoName** 中之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]資料夾和所有子資料夾的內容功能表中使用。 此對話方塊可讓您編寫 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上之所有複寫物件的指令碼。  
  
-   **產生 SQL 指令碼 \<物件名稱>**，這可從發行集和訂閱的內容功能表使用。 此對話方塊可讓您編寫個別物件的指令碼。  
  
 這些對話方塊會編寫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]單一執行個體上之物件的指令碼；它們不會連接到其他執行個體來編寫相關物件的指令碼。  
  
## <a name="generate-sql-script-options"></a>產生 SQL 指令碼選項  
 **散發者屬性**  
 選取即可編寫預存程序的指令碼以：啟用或停用散發者；加入或卸除與散發者相關聯的發行者；以及建立或卸除散發資料庫。  
  
 **下列資料來源中的發行集**  
 選取即可編寫預存程序的指令碼以：啟用或停用發行；建立或卸除發行集、發行項、發送訂閱以及複寫作業。  
  
 **下列資料來源中的訂閱**  
 選取即可編寫預存程序的指令碼，以建立或卸除提取訂閱與複寫作業。  
  
 **[若要建立或啟用元件]** 與 **[若要卸除或停用元件]**  
 指定指令碼是否應包含建立或卸除複寫物件的命令。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您使用對話方塊來建立一組啟用和停用元件的指令碼。  
  
 **複寫作業**  
 選取即可編寫複寫作業的指令碼，但預存程序呼叫除外。 只有從散發者編寫指令碼時，才能使用此選項。  
  
 複寫預存程序會在執行時建立必要的作業，因此不需要選取此選項。 不過，保留建立作業的記錄，在萬一必須重新建立個別作業時非常有用。  
  
## <a name="generate-sql-script-objectname-options"></a>產生 SQL 指令碼選項 \<物件名稱> 選項  
 **[若要建立或啟用元件]** 與 **[若要卸除或停用元件]**  
 指定指令碼是否應包含建立或卸除複寫物件的命令。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您使用對話方塊來建立一組啟用和停用元件的指令碼。  
  
 **複寫作業**  
 只能從 **[產生 SQL 指令碼]** 對話方塊使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [編寫複寫指令碼](../../relational-databases/replication/scripting-replication.md)  
  
  

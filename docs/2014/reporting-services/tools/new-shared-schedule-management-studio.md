---
title: 新增共用排程 (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.newschedule.f1
ms.assetid: b2c69586-d98e-4933-827d-f5e6c15c5203
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 082188276dbc91f52be5813dda5b752c4699e9bf
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59945234"
---
# <a name="new-shared-schedule-management-studio"></a>新增共用排程 (Management Studio)
  您可以使用這個頁面來建立共用排程，以便執行已發行的報表和訂閱。 共用排程可以用來取代報表特定或訂閱特定的排程。 集中式排程資訊以及暫停和繼續排程作業的能力是區別共用排程與項目特有排程的兩個重要功能。  
  
 單一排程中無法支援所有的頻率組合。 例如，若要在每星期五下午 12:00 到下午 4:00。 就必須建立指定星期五為執行日期的兩個每日排程，一個開始時間為下午 12:00， 另一個開始時間為下午 4:00。  
  
 排程處理是以主控和處理排程之報表伺服器的本機時間為基礎。  
  
 若要開啟此頁面，請啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、連線至報表伺服器、以滑鼠右鍵按一下 [共用排程]，然後選取 [新增排程]。 若要儲存排程，SQL Server Agent 服務必須正在執行。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本都提供此功能。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2012 版本支援的功能](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473)。  
  
## <a name="options"></a>選項。  
 **名稱**  
 鍵入共用排程的名稱。 當使用者針對報表和訂閱選取共用排程時，這個名稱會顯示在下拉式清單中。 請務必提供可輕易地容納在清單中而且可輕易地區別共用排程的描述性名稱。 名稱必須至少包含一個英數字元。 它也可以包含空格和某些符號。 指定名稱時，請勿使用下列字元：  
  
 ; ? : \@ & = + , $ / * \< >  
  
 " /  
  
 **開始執行此排程於**  
 指定此排程的開始日期。  
  
 **停止此排程於**  
 指定此排程的到期日。  
  
 **型別**  
 指定循環模式主要是以小時、天、週或月為基礎。  
  
 **小時 (循環模式)**  
 選取選項以便每隔幾個小時的時間執行已排程的作業 (例如，每 6 個小時執行報表一次)。 您可以使用小時和分鐘來指定間隔。  
  
 **天 (循環模式)**  
 選取選項以便每隔幾天的時間執行已排程的作業 (例如，每 2 天執行報表一次)。 您可以使用日來指定間隔，並指定希望排程執行的時間。  
  
 **週 (循環模式)**  
 選取選項以便每隔幾週的時間執行已排程的作業，或是您希望重複執行的模式是以週為基礎時 (例如，每隔一週執行報表一次)。 您可以指定每週的排程，包括執行排程的日子和時間。  
  
 **月 (循環模式)**  
 選取選項以便每隔幾個月的時間執行已排程的作業，或是您希望重複執行的模式是以月為基礎時。 您可以指定每月的排程，包括執行排程的日子和時間。 排程中可以省略特定的月份。  
  
 **一次**  
 選取此選項，即可建立在特定的日期和時間只執行一次的排程。  
  
## <a name="see-also"></a>另請參閱  
 [Management Studio F1 說明中的報表伺服器](report-server-in-management-studio-f1-help.md)   
 [連接至 Management Studio 中的報表伺服器](connect-to-a-report-server-in-management-studio.md)   
 [建立、修改和刪除共用排程](../subscriptions/create-modify-and-delete-schedules.md)   
 [[排程]](../subscriptions/schedules.md)   
 [Management Studio F1 說明中的報表伺服器](report-server-in-management-studio-f1-help.md)  
  
  

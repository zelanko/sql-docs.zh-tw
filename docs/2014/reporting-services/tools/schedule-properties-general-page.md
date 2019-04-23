---
title: 排程屬性 (一般頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.scheduleproperties.general.f1
ms.assetid: 20e43966-6caf-4972-a2e2-0d9131ac8f51
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eaaff2a90f18a4fb7cec3c049945c87fd0a5ed8b
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59966134"
---
# <a name="schedule-properties-general-page"></a>排程屬性 (一般頁面)
  使用此頁面即可檢視或修改共用排程。 共用排程可以用來取代報表特定或訂閱特定的排程。 對排程所做的變更會在您儲存排程之後套用。 編輯排程並不會影響目前正在進行中的作業。 如果您編輯排程時，該排程正在使用中，則系統會允許根據該排程觸發的所有目前處理中報表和訂閱繼續完成。  
  
 單一排程中無法支援所有的頻率組合。 例如，若要在每星期五下午 12:00 到下午 4:00。 就必須建立指定星期五為執行日期的兩個每日排程，一個開始時間為下午 12:00， 另一個開始時間為下午 4:00。  
  
 排程處理是以主控和處理排程之報表伺服器的本機時間為基礎。  
  
 若要開啟此頁面，請啟動[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，連接至報表伺服器，開啟**共用排程**資料夾，以滑鼠右鍵按一下共用的排程，並選取**屬性**。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本都提供此功能，而且在您執行沒有此功能的版本時，此頁面並不會出現。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2012 版本支援的功能](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473)。  
  
## <a name="options"></a>選項。  
 **名稱**  
 指定共用排程的名稱。  
  
 **開始執行此排程於**  
 指定此排程的開始日期。  
  
 **停止此排程於**  
 指定此排程的到期日。  
  
 **型別**  
 指定循環模式主要是以小時、天、週、月為基礎，還是只執行一次。  
  
 **小時 (循環模式)**  
 指定以小時為間隔的選項，來執行排程的作業 (例如，每 6 小時執行報表一次)。 您可以使用小時和分鐘來指定間隔。  
  
 **天 (循環模式)**  
 指定以天數為間隔的選項，來執行排程的作業 (例如，每 2 天執行報表一次)。 您可以使用日來指定間隔，並指定希望排程執行的時間。  
  
 **週 (循環模式)**  
 指定以週為間隔或是以週為基礎的選項，來執行排程的作業 (例如，每隔一週執行報表一次)。 您可以指定每週的排程，包括執行排程的日子和時間。  
  
 **月 (循環模式)**  
 指定以月為間隔或是以月為基礎的選項，來執行排程的作業。 您可以指定每月的排程，包括執行排程的日子和時間。 排程中可以省略特定的月份。  
  
 **一次**  
 指定排程只在特定的日期和時間執行一次。  
  
## <a name="see-also"></a>另請參閱  
 [Management Studio F1 說明中的報表伺服器](report-server-in-management-studio-f1-help.md)   
 [連接至 Management Studio 中的報表伺服器](connect-to-a-report-server-in-management-studio.md)   
 [建立、修改和刪除共用排程](../subscriptions/create-modify-and-delete-schedules.md)   
 [排程](../subscriptions/schedules.md)  
  
  

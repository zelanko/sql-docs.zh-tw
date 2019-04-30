---
title: 排程屬性 (報表頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.scheduleproperties.reports.f1
ms.assetid: 7db728bd-4b08-43ef-a49a-e8dcdd37cf89
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1ddc4ca8fa9a0d6d9a109ccb205bdd9684b2f370
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63158793"
---
# <a name="schedule-properties-reports-page"></a>排程屬性 (報表頁面)
  使用此頁面，即可檢視使用此共用排程之所有報表的清單。 排程可用來重新整理報表快照集、產生報表記錄、觸發訂閱或使報表的快取副本過期。 若要了解如何使用排程，請檢視報表的屬性和訂閱資訊。  
  
 雖然這個頁面會顯示使用此共用排程的每份報表，但是它不會指出在該單一報表內使用此共用排程的次數。 例如，假設 Company Sales 報表的 20 位不同訂閱者都使用相同的共用排程來觸發訂閱處理。 在此情況下，Company Sales 報表只會在此清單中顯示一次，即使報表具有共用排程的 20 個參考也一樣。  
  
 若要開啟此頁面，請啟動[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，連接至報表伺服器，開啟**共用排程**資料夾，以滑鼠右鍵按一下共用的排程，請選取**屬性**，然後按一下 **報表**.  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本都提供此功能。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2012 版本支援的功能](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473)。  
  
## <a name="options"></a>選項。  
 **資料夾**  
 指定報表的路徑。  
  
 **報表**  
 指定使用排程之報表的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [建立、修改和刪除共用排程](../subscriptions/create-modify-and-delete-schedules.md)   
 [排程](../subscriptions/schedules.md)   
 [Management Studio F1 說明中的報表伺服器](report-server-in-management-studio-f1-help.md)   
 [連接至 Management Studio 中的報表伺服器](connect-to-a-report-server-in-management-studio.md)   
 [設定報表的一般屬性&#40;報表管理員&#41;](../configure-general-properties-for-a-report-report-manager.md)  
  
  

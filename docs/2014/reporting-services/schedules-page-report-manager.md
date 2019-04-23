---
title: 排程頁面 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ef19d96e-9f00-4434-950e-152dda9c1ced
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3c232740598e1c9d1f8911c5fa5662d4ef82d5b2
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59948794"
---
# <a name="schedules-page-report-manager"></a>排程頁面 (報表管理員)
  您可以使用 [排程] 頁面來建立、修改、刪除、暫停或繼續執行共用排程。 共用排程是具名的排程，可以和報表、訂閱及消耗排程資訊的其他處理序分開建立和管理。 使用者可以選取您提供的共用排程。  
  
 若要刪除、暫停或繼續執行共用排程，請選取想要修改的共用排程旁邊的核取方塊。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供此功能。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>巡覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
### <a name="to-open-the-schedules-page"></a>若要開啟排程頁面  
  
1.  開啟報表管理員。  
  
2.  在頁面的頂端，按一下右邊角落的 **[站台設定]**。 這樣就會開啟該站台的 [一般] 屬性頁面。  
  
3.  選取 **[排程]** 索引標籤。  
  
## <a name="options"></a>選項。  
 **新的排程**  
 按一下即可開啟 [排程] 頁面，可用來指定頻率資訊。  
  
 **刪除**  
 按一下即可移除共用排程。  
  
 **暫停**  
 按一下即可暫時停止執行共用排程。 暫停排程可避免訂閱及其他已排程處理序的執行。  
  
 **繼續**  
 按一下即可重新恢復共用排程。 不會啟動在暫停排程時排定執行的失效處理序。  
  
 **[排程]**  
 顯示目前定義的共用排程。 按一下共用排程以檢視或編輯頻率資訊。  
  
 **建立者**  
 顯示建立共用排程的使用者名稱。  
  
 **上次執行 / 下一個執行**  
 顯示最後執行共用排程和下一個執行共用排程的時間。  
  
 **狀態**  
 顯示共用排程是否為暫停或使用中。  
  
## <a name="see-also"></a>另請參閱  
 [建立、修改和刪除共用排程](subscriptions/create-modify-and-delete-schedules.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  

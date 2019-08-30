---
title: Data Quality Client 首頁畫面 | Microsoft Docs
ms.custom: ''
ms.date: 02/29/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.clienthome.f1
ms.assetid: 7c6ec469-bc7d-4d19-8e21-11dcf8ade108
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 660c48540bb7d7763eb149c0882f5b37f2cc0d1e
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70152581"
---
# <a name="data-quality-client-home-screen"></a>Data Quality Client 首頁畫面

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  使用這個畫面以存取 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 三大工作群組的使用者介面：知識庫管理、資料品質專案，以及系統管理。  
  
## <a name="options"></a>選項。  
  
### <a name="knowledge-base-management"></a>知識庫管理  
 DQS 知識庫是中繼資料的儲存機制，DQS 使用中繼資料以改善資料品質。 此中繼資料是由 DQS 平台在電腦輔助的知識探索程序中以及資料服務員在互動式定義域管理程序中所建立。  
  
 **新增知識庫**  
 啟動建立知識庫的程序，可以從頭建立或以現有知識庫的中繼資料為基礎。 此命令會開啟一個頁面，您可以在其中識別知識庫、將該知識庫以現有的知識庫為基礎、選取所需的知識庫活動，然後建立該知識庫。  
  
 **開啟知識庫**  
 開啟知識庫讓您可以管理其定義域、執行知識探索、或建立比對原則。 按一下 **[開啟知識庫]** 按鈕可顯示 **[開啟知識庫]** 頁面，此頁面會顯示現有知識庫的清單，及其屬性、目前狀態、知識庫與其定義域的詳細資料。 選取知識庫，然後從 **[開啟知識庫]** 來開啟它。  
  
 **最近使用的知識庫**  
 從畫面上的清單開啟已經建立的知識庫。 如果未鎖定，按一下向右鍵，然後選取您要在其中啟動知識庫的活動 (定義域管理、知識探索或比對原則)。  
  
 您僅能開啟您鎖定的知識庫並進行編輯。 若是如此，知識庫將會以關閉時所處的狀態開啟，並將該狀態顯示在括弧中。 如果某個知識庫遭到鎖定，而且不是您鎖定的，則僅能以唯讀模式開啟該知識庫。  
  
### <a name="data-quality-projects"></a>資料品質專案  
 資料品質專案是 DQS 透過電腦輔助的資料更正和互動式資料清理，執行資料清理或資料比對的程序。  
  
 **新增資料品質專案**  
 啟動建立新專案的專案。 此命令會開啟一個頁面，您可以在其中識別專案、讓該專案與知識庫產生關聯、顯示知識庫的詳細資料、選取所需的專案活動，然後建立該專案。  
  
 **開啟資料品質專案**  
 開啟專案，讓您可以執行資料清理或資料比對。 按一下 **[開啟資料品質專案]** 按鈕可顯示 **[開啟資料品質專案]** 頁面，此頁面會顯示現有專案的清單，及其屬性、目前狀態、知識庫與其定義域和比對原則規則的詳細資料。 選取專案，然後從 **[開啟資料品質專案]** 來開啟它。  
  
 **最近使用的資料品質專案**  
 從畫面上的清單選取已經建立的專案。 您僅能開啟您鎖定的專案。 若是如此，專案將會以關閉時所處的狀態開啟，並將該狀態顯示在括弧中。 如果該專案已完成，將會在活動的「匯出」步驟開啟。  
  
### <a name="administration"></a>系統管理  
 DQS 管理可讓您監視、設定及維護 DQS。  
  
 **活動監控**  
 顯示與連接之 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]相關的所有目前和歷程記錄活動的狀態檢視。 監視的活動類型包含知識管理、資料品質專案和以 SSIS 為基礎的資料更正。  
  
 **Configuration**  
 顯示參考資料服務帳戶的設定屬性 (透過 Azure Marketplace 並直接參考資料服務)、一般設定 (互動式清理、比對和程式碼剖析) 和記錄嚴重性設定。  
  
## <a name="see-also"></a>另請參閱  
 [DQS 知識庫與定義域](../data-quality-services/dqs-knowledge-bases-and-domains.md)   
 [資料品質專案 &#40;DQS&#41;](../data-quality-services/data-quality-projects-dqs.md)   
 [DQS 管理](../data-quality-services/dqs-administration.md)  
  
  

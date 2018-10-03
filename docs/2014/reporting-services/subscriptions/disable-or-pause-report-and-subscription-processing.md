---
title: 暫停報表與訂閱處理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4c15666aecbbdde8ca95eaf684bf9909454d3d42
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129308"
---
# <a name="pause-report-and-subscription-processing"></a>暫停報表與訂閱處理
  您無法直接暫停報表或訂閱。 但是，您可以在處理開始之前，或在進行資料來源連接時，中斷報表與訂閱處理。 您也可以不讓使用者存取報表或訂閱，以禁止處理報表或訂閱。  
  
 下列策略可以用來暫時禁止進行處理。  
  
## <a name="modify-role-assignments-to-prevent-access"></a>修改角色指派來禁止存取  
 讓報表無法使用的最佳方法，是暫時移除可以提供存取報表的角色指派。 無論建立資料來源連接的方式為何，此方法可以用於所有報表。 此方法僅會以報表為目標，不會影響其他報表或項目的作業。  
  
 若要移除角色指派，請在報表管理員中，開啟報表的 [安全性屬性] 頁面。 如果報表從父系繼承安全性，您可以按一下 **[編輯項目安全性]** 來建立嚴格的安全性原則，省略提供普遍存取權的角色指派 (例如，您可以移除提供 Everyone 存取權的角色指派，保留提供一小組使用者存取權的角色指派，例如系統管理員)。  
  
## <a name="disable-a-shared-data-source"></a>停用共用資料來源  
 使用共用資料來源的優點之一是您可以停用它，禁止執行報表或資料驅動訂閱。 停用共用資料來源會中斷報表與其外部來源的連接。 停用時，資料來源無法供所有使用它的報表與訂閱使用。 若要停用共用資料來源，請在報表管理員中開啟資料來源，然後清除 **[啟用此資料來源]** 核取方塊。  
  
 請注意，即使資料來源無法使用，報表仍然會載入。 報表不包含資料，但具備適當權限的使用者可以存取與報表相關聯的屬性頁面、安全性設定、報表記錄，以及訂閱資訊。  
  
## <a name="pause-a-shared-schedule"></a>暫停共用排程  
 如果報表或訂閱從共用排程執行，您可以暫停排程來禁止處理。 由排程驅動的所有報表與訂閱處理，會被延遲至排程繼續為止。 如需詳細資訊，請參閱 <<c0> [ 暫停及繼續共用排程](schedules.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [報表管理員&#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)   
 [安全性屬性頁面，項目 &#40;報表管理員&#41;](../security-properties-page-items-report-manager.md)  
  
  
